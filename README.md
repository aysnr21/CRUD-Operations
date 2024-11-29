# ASP.NET MVC ile CRUD İşlemleri (AJAX ve Bootstrap Kullanarak)

Bu proje, ASP.NET MVC kullanarak CRUD (Create, Read, Update, Delete) işlemlerini gerçekleştirmenin yanı sıra, AJAX ve Bootstrap kullanarak daha dinamik ve kullanıcı dostu bir uygulama geliştirmeyi amaçlamaktadır.

 Proje Özeti

Bu uygulama, bir **Çalışan** (Employee) tablosunu yönetmek için bir web uygulaması sağlar. Kullanıcılar, çalışanları listeleyebilir, yeni çalışan ekleyebilir, mevcut çalışanları güncelleyebilir ve silebilir. CRUD işlemleri, AJAX kullanılarak asenkron bir şekilde gerçekleştirilir, böylece sayfa yeniden yüklenmeden veriler güncellenebilir.

 Özellikler

- **Bootstrap** ile responsive ve modern kullanıcı arayüzü.
- **AJAX** ile sayfa yeniden yüklenmeden veri işlemleri.
- **CRUD** (Create, Read, Update, Delete) işlemleri.
- Veritabanı işlemleri için **ADO.NET** kullanımı.
- **Model-View-Controller** (MVC) mimarisi.

 Teknolojiler

- **ASP.NET MVC 5**
- **Bootstrap 4** (Responsive tasarım için)
- **AJAX** (Asenkron veri yükleme ve güncelleme)
- **ADO.NET** (Veritabanı işlemleri için)
- **SQL Server** (Veritabanı)

 Gereksinimler

- Visual Studio (veya herhangi bir ASP.NET MVC geliştirme ortamı)
- SQL Server
- İnternet Bağlantısı (Bootstrap ve jQuery dosyalarını indirebilmek için)

 Kurulum

1. Projeyi indirin veya klonlayın.
2. Visual Studio'yu açın ve projeyi açın.
3. NuGet Paket Yöneticisi'ni kullanarak **Bootstrap** paketini yükleyin.
4. SQL Server'ı açın ve **Employee** tablosu için aşağıdaki SQL şemalarını kullanarak veritabanınızı oluşturun:
    ```sql
    CREATE TABLE Employee (
        EmployeeID INT PRIMARY KEY IDENTITY,
        Name NVARCHAR(50),
        Age INT,
        State NVARCHAR(50),
        Country NVARCHAR(50)
    );
    ```
5. Veritabanı işlemleri için SQL stored procedure'lerini aşağıdaki gibi oluşturun:
    ```sql
    --Select Employees
    CREATE PROCEDURE SelectEmployee AS
    BEGIN
        SELECT * FROM Employee;
    END
    
    --Insert and Update Employee
    CREATE PROCEDURE InsertUpdateEmployee
    (
        @Id INT,
        @Name NVARCHAR(50),
        @Age INT,
        @State NVARCHAR(50),
        @Country NVARCHAR(50),
        @Action VARCHAR(10)
    )
    AS
    BEGIN
        IF @Action = 'Insert'
        BEGIN
            INSERT INTO Employee (Name, Age, State, Country)
            VALUES (@Name, @Age, @State, @Country);
        END
        IF @Action = 'Update'
        BEGIN
            UPDATE Employee
            SET Name = @Name, Age = @Age, State = @State, Country = @Country
            WHERE EmployeeID = @Id;
        END
    END
    
    --Delete Employee
    CREATE PROCEDURE DeleteEmployee (@Id INT) AS
    BEGIN
        DELETE FROM Employee WHERE EmployeeID = @Id;
    END
    ```
6. `Web.config` dosyasındaki veritabanı bağlantı dizesini (connection string) kendi veritabanı bilgilerinizle güncelleyin.

 Kullanım

1. Uygulamanızı çalıştırın.
2. Ana sayfada çalışanların listelendiği bir tablo göreceksiniz.
3. "Yeni Çalışan Ekle" butonuna tıklayarak yeni bir çalışan ekleyebilirsiniz.
4. Mevcut bir çalışanın bilgilerini güncellemek için "Düzenle" bağlantısına tıklayın.
5. Çalışanı silmek için "Sil" bağlantısına tıklayın.

