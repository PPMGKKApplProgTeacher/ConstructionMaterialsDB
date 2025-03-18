# ConstructionMaterialsDB

Задача: База данни за Магазин за Строителни Материали

I. Създаване на база данни ConstructionMaterialsDB със следните таблици:

1. Products (Продукти)
    
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на продукта
   
    • name (VARCHAR(100), UNIQUE) – име на продукта
   
    • price (DECIMAL(10,2)) – цена на продукта
   
    • category_id (INT, FOREIGN KEY → Categories) – категория на продукта
   
2. Categories (Категории)
   
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на категорията
   
    • name (VARCHAR(100), UNIQUE) – име на категорията
   
3. Suppliers (Доставчици)
   
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на доставчика
   
    • name (VARCHAR(100), UNIQUE) – име на доставчика
   
    • contact_info (VARCHAR(200)) – информация за контакт
   
4. Customers (Клиенти)
   
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на клиента
   
    • name (VARCHAR(100)) – име на клиента
   
    • phone (VARCHAR(20), UNIQUE) – телефонен номер
   
5. Orders (Поръчки)
    
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на поръчката
    
    • customer_id (INT, FOREIGN KEY → Customers) – клиент
    
    • order_date (DATETIME) – дата на поръчката
    
    • total_price (DECIMAL(10,2)) – обща сума
    
6. OrderDetails (Детайли на Поръчки) – много към много между Orders и Products
    
    • id (INT, PRIMARY KEY, IDENTITY)
    
    • order_id (INT, FOREIGN KEY → Orders)
    
    • product_id (INT, FOREIGN KEY → Products)
    
    • quantity (INT) – количество
    
7. SupplierProducts (Продукти на Доставчици) – много към много между Suppliers и Products
    
    • id (INT, PRIMARY KEY, IDENTITY)
    
    • supplier_id (INT, FOREIGN KEY → Suppliers)

    • product_id (INT, FOREIGN KEY → Products)
    
    • supply_price (DECIMAL(10,2)) – цена на доставката
    
8. Employees (Служители)
    
    • id (INT, PRIMARY KEY, IDENTITY) – идентификатор на служителя
    
    • name (VARCHAR(100)) – име на служителя
    
    • position (VARCHAR(50)) – длъжност (касир, управител, склададжия)
   
II. Вмъкване на данни в таблиците:

INSERT INTO Categories (name) VALUES
('Бои и лакове'),
('Цимент и лепила'),
('Инструменти');

INSERT INTO Products (name, price, category_id) VALUES
('Бяла боя', 12.50, 1),
('Цимент 25кг', 9.80, 2),
('Чук 500г', 15.00, 3);

INSERT INTO Suppliers (name, contact_info) VALUES
('Строител ООД', 'ул. Индустриална 5, София'),
('БГ Материали', 'бул. България 12, Пловдив');

INSERT INTO Customers (name, phone) VALUES
('Иван Петров', '0888123456'),
('Мария Иванова', '0899765432');

INSERT INTO Orders (customer_id, order_date, total_price) VALUES
(1, '2025-03-16 10:30:00', 22.30),
(2, '2025-03-16 11:45:00', 15.00);

INSERT INTO OrderDetails (order_id, product_id, quantity) VALUES
(1, 1, 1),
(1, 2, 1),
(2, 3, 1);

INSERT INTO SupplierProducts (supplier_id, product_id, supply_price) VALUES
(1, 1, 10.00),
(2, 2, 8.50);

INSERT INTO Employees (name, position) VALUES
('Георги Димитров', 'Касиер'),
('Петър Николов', 'Управител');

III. Създаване на обектноориентиран модел на базата данни и конзолно приложение

    1. Създайте конзолен проект във Visual Studio.
    
    2. Инсталирайте NuGet пакетите:
    
        ◦ Microsoft.EntityFrameworkCore
        
        ◦ Microsoft.EntityFrameworkCore.SqlServer
        
        ◦ Microsoft.EntityFrameworkCore.Tools
        
    3. От меню Tools → NuGet Package Manager → Package Manager Console, отворете конзолата.
    
    4. Изпълнете командата:
    
       Scaffold-DbContext 'Data Source=YOUR_SERVER;Initial Catalog=ConstructionMaterialsDB;Integrated Security=True;Encrypt=False' Microsoft.EntityFrameworkCore.SqlServer -o Data\Models
       
    5. Разгледайте съдържанието на папката Data\Models.
    
    6. Създайте конзолно приложение, което управлява CRUD операции за продуктите, поръчките и клиентите.
    
    7. (По желание) Конзолното приложение трябва да поддържа функция с автоматично довършване по име на търсения обект с натискане на бутона TAB. Например при работа с таблица “Products” при въвеждане на стринг “Бя” и натоскане на бутон TAB трябва да ни бъде допълнено наименованието “Бяла боя”
