USE [master]
GO
/****** Object:  Database [Kutuphane]    Script Date: 7.05.2024 17:11:48 ******/
CREATE DATABASE [Kutuphane]
 CONTAINMENT = NONE
 ON  PRIMARY 
( NAME = N'Kutuphane', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\MSSQL\DATA\Kutuphane.mdf' , SIZE = 8192KB , MAXSIZE = UNLIMITED, FILEGROWTH = 65536KB )
 LOG ON 
( NAME = N'Kutuphane_log', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\MSSQL\DATA\Kutuphane_log.ldf' , SIZE = 8192KB , MAXSIZE = 2048GB , FILEGROWTH = 65536KB )
 WITH CATALOG_COLLATION = DATABASE_DEFAULT, LEDGER = OFF
GO
ALTER DATABASE [Kutuphane] SET COMPATIBILITY_LEVEL = 160
GO
IF (1 = FULLTEXTSERVICEPROPERTY('IsFullTextInstalled'))
begin
EXEC [Kutuphane].[dbo].[sp_fulltext_database] @action = 'enable'
end
GO
ALTER DATABASE [Kutuphane] SET ANSI_NULL_DEFAULT OFF 
GO
ALTER DATABASE [Kutuphane] SET ANSI_NULLS OFF 
GO
ALTER DATABASE [Kutuphane] SET ANSI_PADDING OFF 
GO
ALTER DATABASE [Kutuphane] SET ANSI_WARNINGS OFF 
GO
ALTER DATABASE [Kutuphane] SET ARITHABORT OFF 
GO
ALTER DATABASE [Kutuphane] SET AUTO_CLOSE OFF 
GO
ALTER DATABASE [Kutuphane] SET AUTO_SHRINK OFF 
GO
ALTER DATABASE [Kutuphane] SET AUTO_UPDATE_STATISTICS ON 
GO
ALTER DATABASE [Kutuphane] SET CURSOR_CLOSE_ON_COMMIT OFF 
GO
ALTER DATABASE [Kutuphane] SET CURSOR_DEFAULT  GLOBAL 
GO
ALTER DATABASE [Kutuphane] SET CONCAT_NULL_YIELDS_NULL OFF 
GO
ALTER DATABASE [Kutuphane] SET NUMERIC_ROUNDABORT OFF 
GO
ALTER DATABASE [Kutuphane] SET QUOTED_IDENTIFIER OFF 
GO
ALTER DATABASE [Kutuphane] SET RECURSIVE_TRIGGERS OFF 
GO
ALTER DATABASE [Kutuphane] SET  DISABLE_BROKER 
GO
ALTER DATABASE [Kutuphane] SET AUTO_UPDATE_STATISTICS_ASYNC OFF 
GO
ALTER DATABASE [Kutuphane] SET DATE_CORRELATION_OPTIMIZATION OFF 
GO
ALTER DATABASE [Kutuphane] SET TRUSTWORTHY OFF 
GO
ALTER DATABASE [Kutuphane] SET ALLOW_SNAPSHOT_ISOLATION OFF 
GO
ALTER DATABASE [Kutuphane] SET PARAMETERIZATION SIMPLE 
GO
ALTER DATABASE [Kutuphane] SET READ_COMMITTED_SNAPSHOT OFF 
GO
ALTER DATABASE [Kutuphane] SET HONOR_BROKER_PRIORITY OFF 
GO
ALTER DATABASE [Kutuphane] SET RECOVERY SIMPLE 
GO
ALTER DATABASE [Kutuphane] SET  MULTI_USER 
GO
ALTER DATABASE [Kutuphane] SET PAGE_VERIFY CHECKSUM  
GO
ALTER DATABASE [Kutuphane] SET DB_CHAINING OFF 
GO
ALTER DATABASE [Kutuphane] SET FILESTREAM( NON_TRANSACTED_ACCESS = OFF ) 
GO
ALTER DATABASE [Kutuphane] SET TARGET_RECOVERY_TIME = 60 SECONDS 
GO
ALTER DATABASE [Kutuphane] SET DELAYED_DURABILITY = DISABLED 
GO
ALTER DATABASE [Kutuphane] SET ACCELERATED_DATABASE_RECOVERY = OFF  
GO
ALTER DATABASE [Kutuphane] SET QUERY_STORE = ON
GO
ALTER DATABASE [Kutuphane] SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30), DATA_FLUSH_INTERVAL_SECONDS = 900, INTERVAL_LENGTH_MINUTES = 60, MAX_STORAGE_SIZE_MB = 1000, QUERY_CAPTURE_MODE = AUTO, SIZE_BASED_CLEANUP_MODE = AUTO, MAX_PLANS_PER_QUERY = 200, WAIT_STATS_CAPTURE_MODE = ON)
GO
USE [Kutuphane]
GO
/****** Object:  Table [dbo].[kitaplar]    Script Date: 7.05.2024 17:11:48 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[kitaplar](
	[kitapNo] [int] IDENTITY(1,1) NOT NULL,
	[kitapAdi] [nvarchar](60) NOT NULL,
	[sayfaSayisi] [int] NOT NULL,
	[yazarNo] [int] NOT NULL,
	[kayitTarihi] [date] NOT NULL,
 CONSTRAINT [PK_kitaplar] PRIMARY KEY CLUSTERED 
(
	[kitapNo] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[yazarlar]    Script Date: 7.05.2024 17:11:48 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[yazarlar](
	[yazarNo] [int] IDENTITY(1,1) NOT NULL,
	[yazar] [ntext] NOT NULL,
 CONSTRAINT [PK_yazarlar] PRIMARY KEY CLUSTERED 
(
	[yazarNo] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
ALTER TABLE [dbo].[kitaplar]  WITH CHECK ADD  CONSTRAINT [FK_kitaplar_yazarlar] FOREIGN KEY([yazarNo])
REFERENCES [dbo].[yazarlar] ([yazarNo])
GO
ALTER TABLE [dbo].[kitaplar] CHECK CONSTRAINT [FK_kitaplar_yazarlar]
GO
USE [master]
GO
ALTER DATABASE [Kutuphane] SET  READ_WRITE 
GO
