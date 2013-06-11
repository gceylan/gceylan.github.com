---
layout: post
title: hibernate
---

### ORM(Object Relational Mapping) ###
ORM, veritabanında oluşturulan her bir nesneye (tabloya) karşılık uygulama tarafında bir nesne oluşturma işidir.

### ORM ile neler yapılabilir? ###
ORM sayesinde SQL sorgularıyla yapılan birçok işlem SQL sorgusu kullanılmadan gerçekleştirilmektedir.

### Java için ORM Frameworkleri ###
	- Hibernate
	- JPA
	- OpenJPA
	- Toplink
	- EclipseLink
	- Apache Cayenne
	- MyBattis

### Hibernate ###

Nesne Yönelimli Programlama(NYP) ve ilişkisel veritabanı kullanımı günümüzde oldukça yaygındır. Hibernate, Java için geliştirilmiş olan nesne/ilişki eşleme işini yapan(ORM), ücretsiz, özgür (_**[LGPL lisansına sahip](http://www.hibernate.org/license)**_) bir yazılımdır.



Tartışmasız, veri tabanına erişim, yani bir kaydı eklemek, silmek, güncellemek
gibi işlemler, kurumsal uygulamaların en önemli bölümünü teşkil etmektedir. Şüphesiz uygulamaların en vakit kaybedici noktaları bu `I/O` işlemleridir.

Hibernate gibi teknolojilerin amacı, kurumsal programcıların veriye erişim
işlemlerini tamamen POJO’lar üzerinden yapmalarına imkan vermeleridir(`POJO -> Plain Old Java Object`). Bir
POJO’nun veri tabanına nasıl eşlenmesi gerektiğini eşleme (mapping) dosyası üzerinden anlayabilen Hibernate, bu noktadan sonra tüm gerekli SQL komutlarını
dinamik olarak arka planda kendisi üretebilecektir. Yani bir tablo
üzerinde JDBC ile yaptığımız `SELECT, UPDATE, INSERT, DELETE` işlemlerinin
tümü, tek bir eşleme dosyası ile Hibernate tarafından otomatik olarak yapılacaktır.

### Bağlantı Havuzları ####
Bağlantı alma işlemi (connection), kurumsal uygulamalarda en pahalı(maliyetli) ve yavaş işlemlerden biri haline gelmektedir. Böyle uygulamalarda sistemin cevap verme hızını arttırmak isteyen programcılar, her işlem başına (transaction) sürekli yeni bir bağlantı açıp, işlem sonunda bu bağlantıları kapatan kodlar yazmaktan kaçınırlar. Bunun yerine, bağlantılar uygulama başında bir kez açılır ve bir tür `bağlantı önbelleği`nda tutularak uygulamanın işleyişi boyunca açık tutulurlar. Bağlantı önbelleği bir nevi havuzdur. Bağlantılar sürekli açılıp kapatılmazlar, sadece bu ortak havuzdan alınıp geri verilirler. Bu bağlantı havuzu sınırlı sayıda bağlantıya izin vermektedir. bağlantı havuzu ve diğer koşullar iyi ayarlandığında uygulama daha performanslı çalışacaktır.

### Örnek Uygulama ###
	Örnek uygulamada mysql veritabanı kullanılmaktadır.
   
Öncelikle bir veritabanı oluşturalım daha sonra bu veritabanına `account` isimli bir tablo ekleyelim.

	account tablosu ACCOUNT_ID(BIGINT), ACCOUNT_TYPE(VARCHAR(200)), CREATION_TYPE(TIMESTAMP) ve BALANCE(BIGINT) hücrelerinden oluşsun.

 Account sınıfımız aşağıdaki gibidir:
<pre><code class="java">
	public class Account {
		
		public static final String ACCOUNT_TYPE_SAVINGS = "SAVINGS";
		public static final String ACCOUNT_TYPE_CHECKING = "CHECKING";
		
		private long accountId;
		private String accountType;
		private Date creationDate;
		private double balance;
		
		public long getAccountId() {
			return accountId;
		}
		
		public void setAccountId(long accountId) {
			this.accountId = accountId;
		}
		
		public String getAccountType() {
			return accountType;
		}
		
		public void setAccountType(String accountType) {
			this.accountType = accountType;
		}
		
		public Date getCreationDate() {
			return creationDate;
		}
		
		public void setCreationDate(Date creationDate) {
			this.creationDate = creationDate;
		}
		
		public double getBalance() {
			return balance;
		}
		
		public void setBalance(double balance) {
			this.balance = balance;
		}
		
		public String toString() {
			StringBuffer sb = new StringBuffer(512);
			
			sb.append("\n----ACCOUNT----\n");
			sb.append("accountId=" + accountId + "\n");
			sb.append("accountType=" + accountType + "\n");
			sb.append("creationDate=" + creationDate + "\n");
			sb.append("balance=" + balance + "\n");
			sb.append("----ACCOUNT----\n");
			
			return sb.toString();
		}
	}
</code></pre>

Account classı ile veritabanındaki account tablosunu eşleyen(mapping) .xml dosyası aşağıdaki gibidir. Bu dosya normal java classlarının üst dizininde olmalıdır.
Aşağıda da gördüğünüz gibi Account sınıfının tüm nesne değişkenleriyle account tablosunun her bir hücresi, hücresel özellikleri de göz önünde bulundurularak eşleştirlmektedir. Alternatif olarak Annotation da kullanabilirsiniz.

	<?xml version="1.0"?>
	<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
	"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
	<!-- Generated 17.May.2013 21:54:45 by Hibernate Tools 3.4.0.CR1 -->
	<hibernate-mapping>
	    <class name="com.gceylan.vo.Account" table="ACCOUNT">
	        <id name="accountId" type="long">
	            <column name="ACCOUNT_ID" />
	            <generator class="assigned" />
	        </id>
	        <property name="accountType" type="java.lang.String">
	            <column name="ACCOUNT_TYPE" />
	        </property>
	        <property name="creationDate" type="java.util.Date">
	            <column name="CREATION_DATE" />
	        </property>
	        <property name="balance" type="double">
	            <column name="BALANCE" />
	        </property>
	    </class>
	</hibernate-mapping>

AccountDAO sınıfı aşağıdaki gibidir:
<pre><code class="java">
	public class AccountDAO {
		
		public void saveOrUpdateAccount(Account account) {
			Session session = HibernateUtil.getSessionFactory().getCurrentSession();
			
			// Remember the number of LOC needed to do this with JDBC?
			session.saveOrUpdate(account);
		}
		
		public Account getAccount(long accountId) {
			Session session = HibernateUtil.getSessionFactory().getCurrentSession();
			Account account = (Account) session.get(Account.class, accountId);
			
			return account;
		}
		
		public void deleteAccount(Account account) {
			Session session = HibernateUtil.getSessionFactory().getCurrentSession();
			session.delete(account);
		}
	}
</code></pre>

AccountService sınıfı:
<pre><code class="java">
	public class AccountService {
		
		AccountDAO accountDAO = new AccountDAO();
		
		public void saveOrUpdateAccount(Account account) {
			accountDAO.saveOrUpdateAccount(account);
		}
		
		public Account getAccount(long accountId) {
			return accountDAO.getAccount(accountId);
		}
		
		public void deleteAccount(Account account) {
			accountDAO.deleteAccount(account);
		}
	}
</code></pre>

HibernateUtil sınıfı:
<pre><code class="java">
	public class HibernateUtil {
		private static final SessionFactory sessionFactory;
		
		static {
			try {
				// Create the SessionFactory from hibernate.cfg.xml
				// SessionFactory is thread-safe (Singleton for the entire application)
				sessionFactory = new Configuration().configure().buildSessionFactory();
			} catch (Throwable ex) {
				System.err.println("Initial SessionFactory creation failed." + ex);
				throw new ExceptionInInitializerError(ex);
			}
		}
		
		public static SessionFactory getSessionFactory() {
			return sessionFactory;
		}
	}
</code></pre>

hibernate.cfg.xml dosyası aşağıdaki gibidir. Burada veritabını connection stringi ve veritabanı bağlantısı için gerekli bilgiler bulunmaktadır. Tüm mappingler bu dosyada belirtilmek zorundadır.

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE hibernate-configuration PUBLIC
			"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
			"http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
	<hibernate-configuration>
		<session-factory>
			<property name="connection.driver_class">com.mysql.jdbc.Driver</property>
			<property name="connection.url">jdbc:mysql://localhost:3306/db_name</property>
			<property name="connection.username">username</property>
			<property name="connection.password">password</property>
			<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
	        
	        <!-- JDBC connection pool (use the built-in) -->
			<property name="connection.pool_size">1</property>
	        
	        <!-- Enable Hibernate's automatic session context management -->
			<property name="current_session_context_class">thread</property>
	
	        <!-- Echo all executed SQL to stdout -->
			<property name="show_sql">true</property>
			<property name="format_sql">false</property>
	
			<!--  Load all mapping files -->
			<mapping resource="Account.hbm.xml" />
		</session-factory>
	</hibernate-configuration>

projeyi oluşturduktan sonra, proje üzerinde sağ tıklayıp properties > java build path > add library tıklayıp, JUnit' i seçerek test için gerekli jarları projeye dahil edebilirsiniz. İsterseniz kendiniz bir main bloğu yazarak da test edebilirsini 

<pre><code class="java">
public class MyJUnitTest extends TestCase {
	
	@Test
	public void testCreateAccount() {
		Session session = HibernateUtil.getSessionFactory().getCurrentSession();
		session.beginTransaction();
		
		Account account = new Account();
		account.setAccountType(Account.ACCOUNT_TYPE_SAVINGS);
		account.setCreationDate(new Date());
		account.setBalance(1000L);
		
		// confirm that there is no accountId set
		Assert.assertTrue(account.getAccountId() == 0);
		
		// save the account
		AccountService accountService = new AccountService();
		accountService.saveOrUpdateAccount(account);
		
		session.getTransaction().commit();
		HibernateUtil.getSessionFactory().close();
		
		System.out.println(account);
		Assert.assertTrue(account.getAccountId() > 0);
	}
}
</code></pre>

örnek uygulamanın kaynak kodları _**[githubtadır.](https://github.com/gceylan/pro-lang/tree/master/java/SimpleHibernateExample)**_