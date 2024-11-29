1. Projeyi Başlatma
Visual Studio'yu Açın
İlk olarak Visual Studio'yu açıyoruz. Projeyi açmak için File > Open > Project/Solution seçeneğini kullanıyoruz ve proje dosyasını seçiyoruz.

Veritabanı Bağlantısını Yapılandırın
Proje, SQL Server veritabanına bağlanıyor. Web.config dosyasındaki bağlantı dizesini, kendi veritabanı bilgilerinizle güncelleyin.

xml
Copy code
<connectionStrings>
    <add name="DBCS" connectionString="Data Source=.;Initial Catalog=EmployeeDB;Integrated Security=True" providerName="System.Data.SqlClient" />
</connectionStrings>
Veritabanını ve Tabloları Oluşturun
SQL Server Management Studio’yu açın ve yeni bir veritabanı (EmployeeDB) oluşturun. Ardından gerekli tabloları ve prosedürleri aşağıdaki SQL kodları ile oluşturun:

Employee Tablosu

sql
Copy code
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY IDENTITY(1,1),
    Name NVARCHAR(100),
    Age INT,
    State NVARCHAR(50),
    Country NVARCHAR(50)
);
Stored Procedure (Veri Listeleme)

sql
Copy code
CREATE PROCEDURE SelectEmployee
AS
BEGIN
    SELECT * FROM Employee;
END;
Projeyi Çalıştırın
Visual Studio'da projeyi başlatmak için F5 tuşuna basarak uygulamanızı çalıştırın. Uygulama tarayıcıda açılacaktır.

2. Kullanılan Teknolojiler
ASP.NET MVC
Bu proje, ASP.NET MVC framework kullanılarak geliştirilmiştir. Model-View-Controller yapısına dayalı olarak veri işlemleri ve görseller ayrılır.

SQL Server
Veritabanı olarak SQL Server kullanıyoruz. Çalışan verileri SQL Server'da saklanır ve ADO.NET ile bu veritabanına bağlanılır.

AJAX
Kullanıcı etkileşimini hızlı bir şekilde sağlamak için AJAX kullanıyoruz. Bu sayede sayfa yeniden yüklenmeden veri işlemleri yapılabilir (CRUD işlemleri).

Bootstrap
Kullanıcı arayüzü tasarımı için Bootstrap framework kullanılmıştır. Bu sayede responsive (mobil uyumlu) bir tasarım elde edilmiştir.

3. Veritabanı Bağlantısı ve CRUD İşlemleri
Veritabanı Bağlantısı
EmployeeDB.cs sınıfında veritabanına bağlanıyoruz. Bağlantı dizesi Web.config dosyasından alınıyor ve SqlConnection ile bağlantı sağlanıyor:

csharp
Copy code
string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
using (SqlConnection con = new SqlConnection(cs))
{
    con.Open();
    SqlCommand com = new SqlCommand("SelectEmployee", con);
    com.CommandType = CommandType.StoredProcedure;
    SqlDataReader rdr = com.ExecuteReader();
}
CRUD İşlemleri

Listeleme: SelectEmployee prosedürü ile tüm çalışanları listeleme.
Ekleme: Kullanıcıdan alınan veriler Insert komutuyla veritabanına eklenir.
Güncelleme: Update komutuyla mevcut çalışan bilgileri güncellenir.
Silme: Delete komutuyla çalışan silinir.
Controller ve View
HomeController.cs sınıfında, AJAX istekleri ile veri işlemleri gerçekleştirilir. Index.cshtml dosyasındaki HTML formu ve tablo üzerinden CRUD işlemleri yapılabilir.

4. Projenin Çalıştırılması
Uygulama Başlatıldığında
Uygulama başladığında, Index.cshtml sayfası kullanıcıya çalışan listesini gösterir. Bu liste AJAX ile alınır ve sayfa yeniden yüklenmeden ekrana yansıtılır.

CRUD İşlemleri

Ekleme: "Add New Employee" butonuna tıklayarak yeni çalışan eklenebilir.
Düzenleme: Çalışanlar listesinde düzenleme yapılabilir.
Silme: Liste üzerinden herhangi bir çalışan silinebilir.
