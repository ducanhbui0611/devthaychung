-- Tạo cơ sở dữ liệu
CREATE DATABASE [PharmacyManagement]
GO

USE [PharmacyManagement]
GO

/****** Object:  Table [dbo].[Admins]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Admins](
	[adminId] [int] IDENTITY(1,1) NOT NULL,
	[username] [nvarchar](50) NOT NULL,
	[password] [nvarchar](255) NOT NULL,
	[name] [nvarchar](100) NOT NULL,
	[email] [nvarchar](100) NOT NULL,
	[phone] [nvarchar](15) NULL,
	[role] [nvarchar](50) NOT NULL,
	[createdAt] [datetime] NOT NULL,
	[updatedAt] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[adminId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY],
UNIQUE NONCLUSTERED 
(
	[username] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Medicines]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Medicines](
	[medicineId] [int] IDENTITY(1,1) NOT NULL,
	[name] [nvarchar](100) NOT NULL,
	[description] [nvarchar](255) NULL,
	[manufacturer] [nvarchar](100) NULL,
	[price] [decimal](10, 2) NOT NULL,
	[costPrice] [decimal](10, 2) NOT NULL,
	[stock] [int] NOT NULL,
	[expiryDate] [date] NOT NULL,
	[usage] [nvarchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[medicineId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Cart]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Cart](
	[cartId] [int] IDENTITY(1,1) NOT NULL,
	[customerId] [int] NOT NULL,
	[medicineId] [int] NOT NULL,
	[quantity] [int] NOT NULL,
	[price] [decimal](10, 2) NOT NULL,
	[addedAt] [datetime] NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[cartId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Customers]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Customers](
	[customerId] [int] IDENTITY(1,1) NOT NULL,
	[name] [nvarchar](100) NOT NULL,
	[phone] [nvarchar](15) NULL,
	[email] [nvarchar](100) NULL,
	[address] [nvarchar](255) NULL,
	[birthday] [date] NULL,
	[password] [nvarchar](255) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[customerId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Employees]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Employees](
	[employeeId] [int] IDENTITY(1,1) NOT NULL,
	[name] [nvarchar](100) NOT NULL,
	[phone] [nvarchar](15) NULL,
	[email] [nvarchar](100) NULL,
	[position] [nvarchar](50) NULL,
	[salary] [decimal](10, 2) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[employeeId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[OrderDetails]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[OrderDetails](
	[orderDetailId] [int] IDENTITY(1,1) NOT NULL,
	[orderId] [int] NOT NULL,
	[medicineId] [int] NOT NULL,
	[quantity] [int] NOT NULL,
	[price] [decimal](10, 2) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[orderDetailId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Orders]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Orders](
	[orderId] [int] IDENTITY(1,1) NOT NULL,
	[customerId] [int] NOT NULL,
	[employeeId] [int] NULL,
	[orderDate] [datetime] NOT NULL,
	[status] [nvarchar](50) NOT NULL,
	[totalAmount] [decimal](10, 2) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[orderId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

/****** Object:  Table [dbo].[Imports]    Script Date: 2/24/2025 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Imports](
	[importId] [int] IDENTITY(1,1) NOT NULL,
	[supplierName] [nvarchar](100) NOT NULL,
	[importDate] [datetime] NOT NULL,
	[medicineId] [int] NOT NULL,
	[quantity] [int] NOT NULL,
	[costPrice] [decimal](10, 2) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[importId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

-- Tạo bảng Category
CREATE TABLE [dbo].[Category](
    [categoryId] [int] IDENTITY(1,1) NOT NULL,
    [categoryName] [nvarchar](100) NOT NULL,
    [description] [nvarchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[categoryId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO

-- Thêm cột categoryId vào bảng Medicines để thiết lập mối quan hệ
ALTER TABLE [dbo].[Medicines] ADD [categoryId] [int] NULL
GO

-- Thiết lập khóa ngoại từ bảng Medicines đến bảng Category
ALTER TABLE [dbo].[Medicines] WITH CHECK ADD FOREIGN KEY([categoryId])
REFERENCES [dbo].[Category] ([categoryId])
GO

-- Thiết lập giá trị mặc định
ALTER TABLE [dbo].[Admins] ADD DEFAULT ('Admin') FOR [role]
GO
ALTER TABLE [dbo].[Admins] ADD DEFAULT (GETDATE()) FOR [createdAt]
GO
ALTER TABLE [dbo].[Medicines] ADD DEFAULT ((0)) FOR [stock]
GO
ALTER TABLE [dbo].[Cart] ADD DEFAULT (GETDATE()) FOR [addedAt]
GO
ALTER TABLE [dbo].[Orders] ADD DEFAULT (GETDATE()) FOR [orderDate]
GO
ALTER TABLE [dbo].[Orders] ADD DEFAULT ('Processing') FOR [status]
GO
ALTER TABLE [dbo].[Imports] ADD DEFAULT (GETDATE()) FOR [importDate]
GO

-- Thiết lập khóa ngoại
ALTER TABLE [dbo].[Cart] WITH CHECK ADD FOREIGN KEY([medicineId])
REFERENCES [dbo].[Medicines] ([medicineId])
GO
ALTER TABLE [dbo].[Cart] WITH CHECK ADD FOREIGN KEY([customerId])
REFERENCES [dbo].[Customers] ([customerId])
GO
INSERT INTO [dbo].[Category] ([categoryName], [description]) VALUES
('Pain Relief', 'Thuốc giảm đau'),
('Antibiotics', 'Kháng sinh'),
('Vitamins', 'Vitamin và chất bổ sung'),
('Cough & Cold', 'Thuốc ho và cảm lạnh');
INSERT INTO [dbo].[Admins] ([username], [password], [name], [email], [phone], [role], [createdAt]) VALUES
('admin1', '1', N'Nguyễn Văn A', 'admin@gmail.com', '0901234567', 'Admin', GETDATE()),
('admin2', 'hashed_password_2', N'Trần Thị B', 'admin2@pharmacy.com', '0912345678', 'Admin', GETDATE());
INSERT INTO [dbo].[Medicines] ([name], [description], [manufacturer], [price], [costPrice], [stock], [expiryDate], [usage], [categoryId]) VALUES
(N'Paracetamol 500mg', N'Giảm đau, hạ sốt', N'PharmaCorp', 5000.00, 3000.00, 100, '2026-12-31', N'Uống 1 viên khi đau', 1),
(N'Ibuprofen 400mg', N'Giảm đau, kháng viêm', N'MediLab', 8000.00, 5000.00, 80, '2025-11-30', N'Uống 1 viên sau ăn', 1),
(N'Aspirin 81mg', N'Chống kết tập tiểu cầu', N'HealthPlus', 3000.00, 2000.00, 150, '2027-01-15', N'Uống 1 viên/ngày', 1),
(N'Amoxicillin 500mg', N'Kháng sinh phổ rộng', N'MediLab', 15000.00, 10000.00, 50, '2025-10-01', N'Uống 2 viên/ngày', 2),
(N'Azithromycin 250mg', N'Kháng sinh điều trị nhiễm khuẩn', N'PharmaCorp', 20000.00, 15000.00, 60, '2026-03-15', N'Uống 1 viên/ngày', 2),
(N'Cefuroxime 500mg', N'Kháng sinh cephalosporin', N'BioHealth', 25000.00, 18000.00, 40, '2025-09-30', N'Uống 2 viên/ngày', 2),
(N'Vitamin C 1000mg', N'Bổ sung vitamin C', N'HealthPlus', 20000.00, 15000.00, 200, '2027-02-20', N'Uống 1 viên/ngày', 3),
(N'Vitamin D3 2000IU', N'Bổ sung vitamin D', N'VitaCare', 25000.00, 20000.00, 120, '2026-11-10', N'Uống 1 viên/ngày', 3),
(N'Multivitamin', N'Bổ sung đa vitamin', N'NutriMax', 30000.00, 22000.00, 90, '2027-05-01', N'Uống 1 viên/ngày', 3),
(N'Syrup Ho Prospan', N'Thuốc trị ho', N'CoughCare', 35000.00, 28000.00, 30, '2025-12-15', N'Uống 10ml/lần', 4),
(N'Decolgen Forte', N'Thuốc cảm cúm', N'PharmaCorp', 6000.00, 4000.00, 100, '2026-01-20', N'Uống 1 viên khi cảm', 4),
(N'Loratadine 10mg', N'Thuốc chống dị ứng', N'AllergyFree', 10000.00, 7000.00, 70, '2026-08-30', N'Uống 1 viên/ngày', 4),
(N'Omeprazole 20mg', N'Giảm axit dạ dày', N'DigestAid', 12000.00, 9000.00, 60, '2025-07-31', N'Uống 1 viên trước ăn', NULL),
(N'Metformin 500mg', N'Điều trị tiểu đường', N'DiabetesCare', 9000.00, 6000.00, 80, '2026-04-15', N'Uống 1 viên sau ăn', NULL),
(N'Atorvastatin 20mg', N'Hạ cholesterol', N'HeartHealth', 15000.00, 11000.00, 50, '2025-11-01', N'Uống 1 viên buổi tối', NULL),
(N'Losartan 50mg', N'Điều trị tăng huyết áp', N'BloodPressureAid', 13000.00, 10000.00, 70, '2026-02-28', N'Uống 1 viên/ngày', NULL),
(N'Diclofenac 50mg', N'Giảm đau khớp', N'PainRelief', 10000.00, 7000.00, 90, '2025-10-10', N'Uống 1 viên sau ăn', 1),
(N'Ciprofloxacin 500mg', N'Kháng sinh điều trị nhiễm khuẩn', N'MediLab', 18000.00, 13000.00, 40, '2025-12-01', N'Uống 2 viên/ngày', 2),
(N'Vitamin B12 500mcg', N'Bổ sung vitamin B12', N'NutriMax', 22000.00, 17000.00, 110, '2027-03-10', N'Uống 1 viên/ngày', 3),
(N'Telfast 180mg', N'Thuốc dị ứng', N'AllergyFree', 15000.00, 11000.00, 60, '2026-06-20', N'Uống 1 viên/ngày', 4),
(N'Panadol Extra', N'Giảm đau mạnh', N'PharmaCorp', 7000.00, 4500.00, 120, '2026-09-15', N'Uống 1 viên khi đau', 1),
(N'Clarithromycin 500mg', N'Kháng sinh điều trị viêm phổi', N'BioHealth', 22000.00, 16000.00, 30, '2025-08-25', N'Uống 1 viên/ngày', 2),
(N'Zinc 50mg', N'Bổ sung kẽm', N'HealthPlus', 18000.00, 14000.00, 150, '2027-04-05', N'Uống 1 viên/ngày', 3),
(N'Benadryl Syrup', N'Thuốc ho và dị ứng', N'CoughCare', 40000.00, 32000.00, 25, '2025-11-20', N'Uống 15ml/lần', 4),
(N'Tramadol 50mg', N'Giảm đau mạnh', N'PainRelief', 12000.00, 9000.00, 60, '2025-09-15', N'Uống 1 viên khi đau', 1),
(N'Levofloxacin 500mg', N'Kháng sinh phổ rộng', N'MediLab', 25000.00, 18000.00, 35, '2026-01-10', N'Uống 1 viên/ngày', 2),
(N'Calcium 600mg', N'Bổ sung canxi', N'VitaCare', 20000.00, 15000.00, 100, '2027-02-15', N'Uống 1 viên/ngày', 3),
(N'Cetirizine 10mg', N'Thuốc chống dị ứng', N'AllergyFree', 8000.00, 6000.00, 80, '2026-07-25', N'Uống 1 viên/ngày', 4),
(N'Naproxen 500mg', N'Giảm đau, kháng viêm', N'PainRelief', 11000.00, 8000.00, 70, '2025-10-20', N'Uống 1 viên sau ăn', 1),
(N'Erythromycin 250mg', N'Kháng sinh điều trị nhiễm khuẩn', N'BioHealth', 14000.00, 10000.00, 50, '2025-12-10', N'Uống 2 viên/ngày', 2),
(N'Omega-3 1000mg', N'Bổ sung dầu cá', N'NutriMax', 35000.00, 28000.00, 90, '2027-06-01', N'Uống 1 viên/ngày', 3),
(N'Fluticasone Spray', N'Xịt mũi trị dị ứng', N'AllergyFree', 45000.00, 38000.00, 20, '2026-03-20', N'Xịt 2 lần/ngày', 4),
(N'Codeine 15mg', N'Giảm đau, trị ho', N'PainRelief', 15000.00, 12000.00, 40, '2025-11-05', N'Uống 1 viên khi cần', 1),
(N'Doxycycline 100mg', N'Kháng sinh điều trị mụn', N'MediLab', 16000.00, 11000.00, 60, '2025-08-30', N'Uống 1 viên/ngày', 2),
(N'Magnesium 400mg', N'Bổ sung magiê', N'HealthPlus', 22000.00, 17000.00, 130, '2027-01-25', N'Uống 1 viên/ngày', 3),
(N'Pseudoephedrine 60mg', N'Thuốc thông mũi', N'CoughCare', 9000.00, 7000.00, 90, '2026-05-10', N'Uống 1 viên khi nghẹt', 4),
(N'Meloxicam 15mg', N'Giảm đau khớp', N'PainRelief', 13000.00, 10000.00, 50, '2025-10-25', N'Uống 1 viên sau ăn', 1),
(N'Ceftriaxone 1g', N'Kháng sinh tiêm', N'BioHealth', 30000.00, 25000.00, 20, '2025-09-01', N'Tiêm 1 liều/ngày', 2),
(N'Iron 65mg', N'Bổ sung sắt', N'VitaCare', 18000.00, 14000.00, 100, '2027-03-15', N'Uống 1 viên/ngày', 3),
(N'Dextromethorphan Syrup', N'Thuốc ho khan', N'CoughCare', 32000.00, 26000.00, 35, '2025-12-20', N'Uống 10ml/lần', 4),
(N'Ketoprofen 100mg', N'Giảm đau mạnh', N'PainRelief', 14000.00, 11000.00, 60, '2025-11-15', N'Uống 1 viên sau ăn', 1),
(N'Moxifloxacin 400mg', N'Kháng sinh điều trị viêm phổi', N'MediLab', 28000.00, 22000.00, 25, '2026-02-10', N'Uống 1 viên/ngày', 2),
(N'Vitamin E 400IU', N'Bổ sung vitamin E', N'NutriMax', 25000.00, 20000.00, 80, '2027-04-20', N'Uống 1 viên/ngày', 3),
(N'Salbutamol 2mg', N'Thuốc giãn phế quản', N'AsthmaCare', 6000.00, 4000.00, 100, '2026-06-15', N'Uống 1 viên khi cần', NULL),
(N'Prednisolone 5mg', N'Kháng viêm corticosteroid', N'BioHealth', 8000.00, 6000.00, 70, '2025-10-05', N'Uống theo chỉ định', NULL),
(N'Ranitidine 150mg', N'Giảm axit dạ dày', N'DigestAid', 10000.00, 8000.00, 90, '2026-01-30', N'Uống 1 viên trước ăn', NULL),
(N'Simvastatin 20mg', N'Hạ cholesterol', N'HeartHealth', 12000.00, 9000.00, 60, '2025-12-25', N'Uống 1 viên buổi tối', NULL),
(N'Amlodipine 5mg', N'Điều trị tăng huyết áp', N'BloodPressureAid', 11000.00, 8500.00, 80, '2026-03-05', N'Uống 1 viên/ngày', NULL),
(N'Guaifenesin Syrup', N'Thuốc long đờm', N'CoughCare', 30000.00, 24000.00, 40, '2025-11-25', N'Uống 10ml/lần', 4),
(N'Tylenol 325mg', N'Giảm đau nhẹ', N'PharmaCorp', 6000.00, 4000.00, 110, '2026-07-10', N'Uống 1 viên khi đau', 1);
INSERT INTO [dbo].[Customers] ([name], [phone], [email], [address], [birthday], [password]) VALUES
(N'Lê Văn C', '0933456789', 'customer1@gmail.com', N'123 Đường Láng, Hà Nội', '1990-05-20', 'hashed_password_3'),
(N'Phạm Thị D', '0944567890', 'customer2@gmail.com', N'45 Nguyễn Huệ, TP.HCM', '1985-08-15', 'hashed_password_4');
INSERT INTO [dbo].[Employees] ([name], [phone], [email], [position], [salary]) VALUES
(N'Nguyễn Thị E', '0955678901', 'employee1@pharmacy.com', N'Nhân viên bán hàng', 8000000.00),
(N'Trần Văn F', '0966789012', 'employee2@pharmacy.com', N'Quản lý kho', 10000000.00);
INSERT INTO [dbo].[Imports] ([supplierName], [importDate], [medicineId], [quantity], [costPrice]) VALUES
(N'Công ty PharmaCorp', GETDATE(), 1, 50, 3000.00),
(N'Công ty MediLab', GETDATE(), 2, 30, 10000.00);
INSERT INTO [dbo].[Orders] ([customerId], [employeeId], [orderDate], [status], [totalAmount]) VALUES
(1, 1, GETDATE(), 'Processing', 25000.00),
(2, 2, GETDATE(), 'Completed', 45000.00);
INSERT INTO [dbo].[OrderDetails] ([orderId], [medicineId], [quantity], [price]) VALUES
(1, 1, 5, 5000.00),
(2, 3, 2, 20000.00),
(2, 4, 1, 30000.00);
INSERT INTO [dbo].[Cart] ([customerId], [medicineId], [quantity], [price], [addedAt]) VALUES
(1, 2, 3, 15000.00, GETDATE()),
(2, 1, 10, 5000.00, GETDATE());
ALTER TABLE [dbo].[Medicines]
ADD [image] VARBINARY(MAX) NULL;
GO
