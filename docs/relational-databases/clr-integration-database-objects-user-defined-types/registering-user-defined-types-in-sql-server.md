---
title: 在 SQL Server 中註冊使用者自訂類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4d9eb0f5e08a67036ede2567965e1400494455f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72907502"
---
# <a name="registering-user-defined-types-in-sql-server"></a>在 SQL Server 中註冊使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用使用者定義型別（UDT），您必須註冊它。 註冊 UDT 包括註冊組件，以及在要使用該型別的資料庫中建立它。 UDT 的使用範圍為單一資料庫，而且除非已經向每個資料庫註冊相同的組件及 UDT，否則無法在多個資料庫中使用。 一旦註冊 UDT 組件並建立此型別之後，您便可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 及用戶端程式碼中使用該 UDT。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
## <a name="using-visual-studio-to-deploy-udts"></a>使用 Visual Studio 部署 UDT  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 是部署 UDT 最簡單的方式。 但是，若為較複雜的部署案例而且需要最大的彈性，請使用本主題稍後將要討論的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 請遵循下列步驟，使用 Visual Studio 建立及部署 UDT：  
  
1.  在**Visual Basic**或**Visual c #** 語言節點中建立新的**資料庫**專案。  
  
2.  加入將包含 UDT 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的參考。  
  
3.  加入**使用者定義型**別類別。  
  
4.  撰寫程式碼以實作 UDT。  
  
5.  從 [**建立**] 功能表中，選取 [**部署**]。 如此將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中註冊組件並建立型別。  

## <a name="using-transact-sql-to-deploy-udts"></a>使用 Transact-SQL 部署 UDT  
 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 語法，於要使用 UDT 的資料庫中註冊組件。 它會儲存於資料庫系統資料表內部，而非檔案系統外部。 如果 UDT 與外部組件相關，也必須將它們載入資料庫。 CREATE TYPE 陳述式可在要使用 UDT 的資料庫內建立 UDT。 如需詳細資訊，請參閱[CREATE ASSEMBLY &#40;transact-sql&#41;](../../t-sql/statements/create-assembly-transact-sql.md)和[Create TYPE &#40;transact-sql&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
### <a name="using-create-assembly"></a>使用 CREATE ASSEMBLY  
 CREATE ASSEMBLY 語法會在要使用 UDT 的資料庫中註冊組件。 一旦註冊此組件，它就不具有相依性。  
  
 不允許在給定資料庫內建立同一組件的多個版本。 但是，根據給定資料庫中的文化特性建立相同組件的多個版本是可行的。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內所註冊的不同名稱來區分某個組件的多個文化特性版本。 如需詳細資訊，請參閱 .NET Framework SDK 中的＜建立和使用強式名稱的組件＞。  
  
 當使用 SAFE 或 EXTERNAL_ACCESS 權限集合執行 CREATE ASSEMBLY 時，系統會檢查組件，以確定它可進行驗證且型別是安全的。 如果您省略指定使用權限集合，則會假設為 SAFE。 系統不會檢查使用 UNSAFE 權限集合的程式碼。 如需有關組件權限集合的詳細資訊，請參閱[設計組件](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
#### <a name="example"></a>範例  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]語句會使用 SAFE 許可權集合， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在**AdventureWorks**資料庫中註冊 Point 元件。 如果省略 WITH PERMISSION_SET 子句，將會使用 SAFE 權限集合註冊該組件。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]語句會使用 FROM 子句中的 *<assembly_bits>* 引數來註冊元件。 這個**Varbinary**值將檔案表示為位元組資料流程。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>使用 CREATE TYPE  
 一旦將組件載入資料庫，即可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 陳述式建立此型別。 這樣會將該型別加入該資料庫的可用型別清單。 該型別具有資料庫範圍，而且只能在建立它的資料庫中使用。 如果資料庫中已存在 UDT，則 CREATE TYPE 陳述式會失敗並出現錯誤。  
  
> [!NOTE]  
>  CREATE TYPE 語法也用來建立原生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]別名資料類型，而且是用來將**sp_addtype**取代為建立別名資料類型的方法。 CREATE TYPE 語法中的某些選擇性引數會參考建立 UDT，且不適用於建立別名資料類型 (如基底類型)。  
  
 如需詳細資訊，請參閱[CREATE TYPE &#40;transact-sql&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
#### <a name="example"></a>範例  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]語句會建立**Point**類型。 外部名稱是使用*AssemblyName*的兩部分命名語法來指定。*UDTName*。  
  
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
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 必須以下列順序執行。 首先，參考**點**UDT 的資料表必須卸載，然後是型別，最後是元件。  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>尋找 UDT 相依性  
 如果有相依物件存在 (如具有 UDT 資料行定義的資料表)，則 DROP TYPE 陳述式會失敗。 如果資料庫中有使用 WITH SCHEMABINDING 子句所建立的函數、預存程序或觸發程序，而且這些常式使用使用者定義型別的變數或參數，該陳述式也會失敗。 您必須先卸除所有相依物件，然後再執行 DROP TYPE 陳述式。  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢會尋找在**AdventureWorks**資料庫中使用 UDT 的所有資料行和參數。  
  
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
 當您變更並重新編譯 UDT 組件中的原始程式碼之後，可以使用 ALTER ASSEMBLY 陳述式。 它會將此 .dll 檔案複製到伺服器，並重新繫結至新的組件。 如需完整的語法，請參閱[ALTER ASSEMBLY &#40;transact-sql&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式會從指定的磁碟位置重新載入 Point.dll 組件。  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>使用 ALTER ASSEMBLY 加入原始程式碼  
 ALTER ASSEMBLY 語法中的 ADD FILE 子句不存在於 CREATE ASSEMBLY 中。 您可以使用它來加入原始程式碼，或與組件相關聯的任何其他檔案。 這些檔案會從原始位置複製，並儲存在資料庫的系統資料表中。 如此可在您需要重新建立或記載 UDT 的目前版本時，確保您一定有原始程式碼或其他檔案可用。  
  
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 語句會為**Point** UDT 加入 Point.cs 類別原始程式碼。 這會複製 Point.cs 檔案中包含的文字，並將它儲存在名為 PointSource 的資料庫中。  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 元件資訊儲存在已安裝元件之資料庫的**sys.databases assembly_files**資料表中。 **Assembly_files**資料表包含下列資料行。  
  
 **assembly_id**  
 為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。  
  
 **name**  
 物件的名稱。  
  
 **file_id**  
 識別每個物件的數位，其中第一個物件與給定的**assembly_id**相關聯，而其值為1。 如果有多個物件與相同的**assembly_id**相關聯，則每個後續的**file_id**值都會遞增1。  
  
 **content**  
 組件或檔案的十六進位表示法。  
  
 您可以使用 CAST 或 CONVERT 函數，將**content**資料行的內容轉換成可讀取的文字。 下列查詢會將 Point.cs 檔案的內容轉換為可讀取的文字，並在 WHERE 子句中使用此名稱，以將結果集限制為單一資料列。  
  
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
 **AdventureWorks**範例資料庫中的**Currency** UDT 提供了一種實用的範例，說明如何將 udt 及其相關聯的函式進行結構。 **貨幣**UDT 是用來根據特定文化特性的貨幣系統來處理 money，並允許儲存不同的貨幣類型，例如美元、歐元等等。 UDT 類別會將文化特性名稱公開為字串，並以**decimal**資料類型的形式來呈現貨幣金額。 所有必要的序列化方法都包含在定義類別的組件中。 函式，可將貨幣從某個文化特性轉換成另一個文化特性，並實作為名為**ConvertCurrency**的外部函數，而此函數位于不同的元件中。 **ConvertCurrency**函數會藉由從**AdventureWorks**資料庫中的資料表抓取轉換速率來執行其工作。 如果轉換率的來源應該變更，或如果現有的程式碼有任何其他變更，則可以輕鬆地修改元件，而不會影響**Currency** UDT。  
  
 您可以藉由安裝 common language runtime （CLR）範例，找到**Currency** UDT 和**ConvertCurrency**函式的程式代碼清單。  
  
### <a name="using-udts-across-databases"></a>跨資料庫使用 UDT  
 根據定義，UDT 屬於單一資料庫的範圍。 因此，在一個資料庫內定義的 UDT 無法用於其他資料庫中的資料行定義。 為了在多個資料庫中使用 UDT，您必須在每個資料庫內的相同組件上執行 CREATE ASSEMBLY 及 CREATE TYPE 陳述式。 具有相同名稱、強式名稱、文化特性、版本、使用權限集合及二進位內容的組件，會視為相同組件。  
  
 一旦在兩個資料庫中登錄 UDT 並可存取 UDT，您便可從某個資料庫轉換 UDT 值，以用於另一資料庫。 在下列情況下，可以跨資料庫使用相同的 UDT：  
  
-   呼叫不同資料庫中定義的預存程序。  
  
-   查詢不同資料庫中定義的資料表。  
  
-   從某個資料庫資料表 UDT 資料行選取 UDT 資料，並將其插入具有相同 UDT 資料行的第二個資料庫中。  
  
 在這些情況下，伺服器所需的任何轉換都會自動發生。 您將無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 或 CONVERT 函數明確地執行轉換。  
  
 請注意，在[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] **tempdb**系統資料庫中建立工作資料表時，您不需要採取任何動作來使用 udt。 這包括處理資料指標、資料表變數，以及使用者定義的資料表值函式，這些函數包含 Udt，而且會以透明的方式使用**tempdb**。 不過，如果您在**tempdb**中明確建立定義 UDT 資料行的臨時表，則 UDT 必須以和使用者資料庫相同的方式，在**tempdb**中註冊。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
