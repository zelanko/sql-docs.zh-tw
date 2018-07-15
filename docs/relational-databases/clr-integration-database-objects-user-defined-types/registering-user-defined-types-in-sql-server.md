---
title: SQL Server 中註冊使用者定義型別 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cb3c8321be447d839242ebd8dae18871d0a6c17f
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352200"
---
# <a name="registering-user-defined-types-in-sql-server"></a>在 SQL Server 中註冊使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要使用的使用者定義的型別 (UDT) 中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須註冊它。 註冊 UDT 包括註冊組件，以及在要使用該型別的資料庫中建立它。 UDT 的使用範圍為單一資料庫，而且除非已經向每個資料庫註冊相同的組件及 UDT，否則無法在多個資料庫中使用。 一旦註冊 UDT 組件並建立此型別之後，您便可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 及用戶端程式碼中使用該 UDT。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
## <a name="using-visual-studio-to-deploy-udts"></a>使用 Visual Studio 部署 UDT  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 是部署 UDT 最簡單的方式。 但是，若為較複雜的部署案例而且需要最大的彈性，請使用本主題稍後將要討論的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 請遵循下列步驟，使用 Visual Studio 建立及部署 UDT：  
  
1.  建立新**資料庫**專案中**Visual Basic**或是**Visual C#** 語言節點。  
  
2.  加入將包含 UDT 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的參考。  
  
3.  新增**使用者定義型別**類別。  
  
4.  撰寫程式碼以實作 UDT。  
  
5.  從**建置**功能表上，選取**部署**。 如此將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中註冊組件並建立型別。  
  
## <a name="using-transact-sql-to-deploy-udts"></a>使用 Transact-SQL 部署 UDT  
 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 語法，於要使用 UDT 的資料庫中註冊組件。 它會儲存於資料庫系統資料表內部，而非檔案系統外部。 如果 UDT 與外部組件相關，也必須將它們載入資料庫。 CREATE TYPE 陳述式可在要使用 UDT 的資料庫內建立 UDT。 如需詳細資訊，請參閱[CREATE ASSEMBLY &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/create-assembly-transact-sql.md)並[CREATE TYPE &#40;-&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
### <a name="using-create-assembly"></a>使用 CREATE ASSEMBLY  
 CREATE ASSEMBLY 語法會在要使用 UDT 的資料庫中註冊組件。 一旦註冊此組件，它就不具有相依性。  
  
 不允許在給定資料庫內建立同一組件的多個版本。 但是，根據給定資料庫中的文化特性建立相同組件的多個版本是可行的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內所註冊的不同名稱來區分某個組件的多個文化特性版本。 如需詳細資訊，請參閱 .NET Framework SDK 中的＜建立和使用強式名稱的組件＞。  
  
 當使用 SAFE 或 EXTERNAL_ACCESS 權限集合執行 CREATE ASSEMBLY 時，系統會檢查組件，以確定它可進行驗證且型別是安全的。 如果您省略指定使用權限集合，則會假設為 SAFE。 系統不會檢查使用 UNSAFE 權限集合的程式碼。 如需有關組件權限集合的詳細資訊，請參閱[設計組件](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
#### <a name="example"></a>範例  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式註冊中的點組件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中**AdventureWorks**資料庫，具有 SAFE 權限集合。 如果省略 WITH PERMISSION_SET 子句，將會使用 SAFE 權限集合註冊該組件。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式註冊使用的組件 *< assembly_bits> >* FROM 子句中的引數。 這**varbinary**值表示為位元組資料流的檔案。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 … 21ac78  
```  
  
### <a name="using-create-type"></a>使用 CREATE TYPE  
 一旦將組件載入資料庫，即可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 陳述式建立此型別。 這樣會將該型別加入該資料庫的可用型別清單。 該型別具有資料庫範圍，而且只能在建立它的資料庫中使用。 如果資料庫中已存在 UDT，則 CREATE TYPE 陳述式會失敗並出現錯誤。  
  
> [!NOTE]  
>  CREATE TYPE 語法也用來建立原生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]別名資料類型，而用來取代**sp_addtype**做為建立別名資料類型。 CREATE TYPE 語法中的某些選擇性引數會參考建立 UDT，且不適用於建立別名資料類型 (如基底類型)。  
  
 如需詳細資訊，請參閱 < [CREATE TYPE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
#### <a name="example"></a>範例  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式會建立**點**型別。 EXTERNAL NAME 使用兩部分命名語法的指定*AssemblyName*。*UDTName*。  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>從資料庫移除 UDT  
 DROP TYPE 陳述式會從目前資料庫移除 UDT。 一旦卸除 UDT 之後，您就可以使用 DROP ASSEMBLY 陳述式，從資料庫中卸除組件。  
  
 在下列情況下，將不會執行 DROP TYPE 陳述式：  
  
-   資料庫中包含使用 UDT 定義之資料行的資料表。  
  
-   使用 WITH SCHEMABINDING 子句在資料庫中建立的函數、預存程序或觸發程序 (這些項目會使用 UDT 變數或參數)。  
  
### <a name="example"></a>範例  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 必須以下列順序執行。 第一個資料表會參考**點**UDT 必須先卸除，然後是型別和最後是組件。  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>尋找 UDT 相依性  
 如果有相依物件存在 (如具有 UDT 資料行定義的資料表)，則 DROP TYPE 陳述式會失敗。 如果資料庫中有使用 WITH SCHEMABINDING 子句所建立的函數、預存程序或觸發程序，而且這些常式使用使用者定義型別的變數或參數，該陳述式也會失敗。 您必須先卸除所有相依物件，然後再執行 DROP TYPE 陳述式。  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢找出使用 UDT 中的參數與資料行的所有**AdventureWorks**資料庫。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>維護 UDT  
 一旦在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立 UDT，便無法對其進行修改，但可以改變此型別所依據的組件。 在大多數情況下，您必須使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE 陳述式從資料庫中移除 UDT、對基礎組件進行變更，並使用 ALTER ASSEMBLY 陳述式將其重新載入。 然後需要重新建立 UDT 及一切相依物件。  
  
### <a name="example"></a>範例  
 當您變更並重新編譯 UDT 組件中的原始程式碼之後，可以使用 ALTER ASSEMBLY 陳述式。 它會將此 .dll 檔案複製到伺服器，並重新繫結至新的組件。 如需完整語法，請參閱[ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式會從指定的磁碟位置重新載入 Point.dll 組件。  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>使用 ALTER ASSEMBLY 加入原始程式碼  
 ALTER ASSEMBLY 語法中的 ADD FILE 子句不存在於 CREATE ASSEMBLY 中。 您可以使用它來加入原始程式碼，或與組件相關聯的任何其他檔案。 這些檔案會從原始位置複製，並儲存在資料庫的系統資料表中。 如此可在您需要重新建立或記載 UDT 的目前版本時，確保您一定有原始程式碼或其他檔案可用。  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]ALTER ASSEMBLY 陳述式加入 Point.cs 類別原始程式碼，如**點**UDT。 這會複製 Point.cs 檔案中包含的文字，並將它儲存在名為 PointSource 的資料庫中。  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 組件資訊會儲存在**sys.assembly_files**資料庫已安裝的組件中的資料表。 **Sys.assembly_files**資料表包含下列資料行。  
  
 **assembly_id**  
 為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。  
  
 **name**  
 物件的名稱。  
  
 **file_id**  
 數字，識別每個相關聯的第一個物件的物件，指定**assembly_id** 1 的值。 如果有多個物件具有相同相關聯**assembly_id**，則每個後續**file_id**值都會遞增 1。  
  
 **內容**  
 組件或檔案的十六進位表示法。  
  
 您可以使用 CAST 或 CONVERT 函數，將轉換的內容**內容**可讀取的文字資料行。 下列查詢會將 Point.cs 檔案的內容轉換為可讀取的文字，並在 WHERE 子句中使用此名稱，以將結果集限制為單一資料列。  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 如果您將結果複製並貼至文字編輯器中，將會看到原始檔案中的分行符號及空格均已保留。  
  
## <a name="managing-udts-and-assemblies"></a>管理 UDT 及組件  
 當規劃 UDT 實作時，請考量 UDT 組件本身需要哪些方法，以及哪些方法應在個別組件中建立，並將其實作為使用者定義函數還是預存程序。 將各方法劃分到不同組件，可讓您在更新程式碼時不會影響可能儲存在資料表之 UDT 資料行中的資料。 只有當新的定義可以讀取先前的值且型別的簽章未變更時，您才可以在不卸除 UDT 資料行及其他相依物件的情況下修改 UDT 組件。  
  
 將可能會發生變更的程序性程式碼與實作 UDT 所需的程式碼分開，可以大幅簡化維護作業。 只包含 UDT 運作所需的程式碼並使您的 UDT 定義盡量簡單，這樣就會減少因程式碼修訂或錯誤修復而需要從資料庫卸除 UDT 本身的風險。  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Currency UDT 及貨幣轉換函數  
 **貨幣**中的 UDT **AdventureWorks**範例資料庫提供結構化 UDT 及其相關聯的函式的建議方式的實用範例。 **貨幣**UDT 用於處理特定的文化特性的貨幣系統為基礎的貨幣，並允許儲存不同貨幣類型，如美元、 歐元，等等。 UDT 類別會公開的文化特性名稱做為字串，而將做為貨幣金額**十進位**資料型別。 所有必要的序列化方法都包含在定義類別的組件中。 實作一個不因文化特性的貨幣轉換到另一個函式會實作為名為外部函式**ConvertCurrency**，且此函式位於不同的組件。 **ConvertCurrency**函式會從中的資料表擷取轉換比率**AdventureWorks**資料庫。 如果轉換比率的來源應該變更，或如果應該對現有的程式碼的任何其他變更，可以不會影響輕鬆修改組件**貨幣**UDT。  
  
 程式碼清單**貨幣**UDT 並**ConvertCurrency**函式即可找出安裝 common language runtime (CLR) 範例。  
  
### <a name="using-udts-across-databases"></a>跨資料庫使用 UDT  
 根據定義，UDT 屬於單一資料庫的範圍。 因此，在一個資料庫內定義的 UDT 無法用於其他資料庫中的資料行定義。 為了在多個資料庫中使用 UDT，您必須在每個資料庫內的相同組件上執行 CREATE ASSEMBLY 及 CREATE TYPE 陳述式。 具有相同名稱、強式名稱、文化特性、版本、使用權限集合及二進位內容的組件，會視為相同組件。  
  
 一旦在兩個資料庫中登錄 UDT 並可存取 UDT，您便可從某個資料庫轉換 UDT 值，以用於另一資料庫。 在下列情況下，可以跨資料庫使用相同的 UDT：  
  
-   呼叫不同資料庫中定義的預存程序。  
  
-   查詢不同資料庫中定義的資料表。  
  
-   從某個資料庫資料表 UDT 資料行選取 UDT 資料，並將其插入具有相同 UDT 資料行的第二個資料庫中。  
  
 在這些情況下，伺服器所需的任何轉換都會自動發生。 您將無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 或 CONVERT 函數明確地執行轉換。  
  
 請注意，不需要採取任何動作來使用 Udt 時[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中建立工作資料表中的**tempdb**系統資料庫。 這包括處理的資料指標、 資料表變數和使用者定義資料表值函式，明確地包含 Udt 以及以讓使用**tempdb**。 不過，如果您明確地建立中的暫存資料表**tempdb**可定義 UDT 資料行，則必須在中註冊的 UDT **tempdb**與使用者資料庫相同的方式。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
