---
title: "OPENDATASOURCE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd106322dfc78186aefaadac42622852d87d40f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供特定連接資訊做為四部分物件名稱，而不使用連結伺服器名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>引數  
 *provider_name*  
 這是登錄為 OLE DB 提供者之 PROGID 的名稱，以用來存取資料來源。 *provider_name*是**char**資料型別，而且沒有預設值。  
  
 *init_string*  
 連接字串會傳遞至目的地提供者的 IDataInitialize 介面。 提供者字串語法根據關鍵字-值配對，並以分號分隔，例如： **'***keyword1*=*值***;***keyword2*=*值***'**。  
  
 如需在提供者上支援的特定關鍵字-值配對，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK。 這份文件集定義基本語法。 下表中列出最常用的關鍵字*init_string*引數。  
  
|關鍵字|OLE DB 屬性|有效值和描述|  
|-------------|---------------------|----------------------------------|  
|資料來源|DBPROP_INIT_DATASOURCE|要連接的資料來源名稱。 不同提供者以不同方式解譯這個名稱。 如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，這表示伺服器的名稱。 如果是 Jet OLE DB 提供者，這表示 .mdb 檔或 .xls 檔的完整路徑。|  
|位置|DBPROP_INIT_LOCATION|要連接的資料庫位置。|  
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|提供者特定連接字串。|  
|連接逾時|DBPROP_INIT_TIMEOUT|逾時值，在此之後連接嘗試會失敗。|  
|使用者識別碼|DBPROP_AUTH_USERID|用於連接的使用者識別碼。|  
|密碼|DBPROP_AUTH_PASSWORD|用於連接的密碼。|  
|目錄|DBPROP_INIT_CATALOG|連接到資料來源的初始或預設目錄名稱。|  
|整合式安全性|DBPROP_AUTH_INTEGRATED|SSPI，用來指定 Windows 驗證|  
  
## <a name="remarks"></a>備註  
 唯有針對指定的提供者將 DisallowAdhocAccess 登錄選項明確設為 0 時，且已啟用 [特定分散式查詢] 進階組態選項時，才可使用 OPENDATASOURCE 來存取 OLE DB 資料來源的遠端資料。 若未設定這些選項，預設行為便不允許特定存取。  
  
 OPENDATASOURCE 函數可使用於與連結伺服器名稱相同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法位置。 因此，OPENDATASOURCE 可做為四部分名稱的第一部分使用，來參考 SELECT、INSERT、UPDATE 或 DELETE 陳述式中的資料表或檢視名稱，或參考 EXECUTE 陳述式中的遠端預存程序。 執行遠端預存程序時，OPENDATASOURCE 應該參考 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一個執行個體。 OPENDATASOURCE 不接受變數做為其引數。  
  
 如同 OPENROWSET 函數，OPENDATASOURCE 只應該參考不常存取的 OLE DB 資料來源。 請為存取多次的資料來源定義連結伺服器。 OPENDATASOURCE 或 OPENROWSET 都不提供連結伺服器定義的所有功能，例如安全性管理和查詢目錄資訊的能力。 每次在呼叫 OPENDATASOURCE 時，都必須提供所有連接資訊，包括密碼在內。  
  
> [!IMPORTANT]  
>  Windows 驗證比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證更安全。 可能的話，您應該使用 Windows 驗證。 OPENDATASOURCE 不應與連接字串中的明確密碼一起使用。  
  
 每一個提供者的連接需求都類似於建立連結伺服器時的參數需求。 許多常見提供者的詳細資料會列於主題[sp_addlinkedserver &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 FROM 子句中 OPENDATASOURCE、OPENQUERY 或 OPENROWSET 的任何呼叫都會與當做更新目標使用之這些函數的任何呼叫進行個別且獨立的評估，即使完全相同的引數套用至這兩種呼叫也一樣。 尤其，針對其中一個呼叫結果所套用的篩選或聯結條件對於另一個呼叫的結果沒有作用。  
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以執行 OPENDATASOURCE。 您可以從連接字串判斷用來連接到遠端伺服器的權限。  
  
## <a name="examples"></a>範例  
 下列範例對伺服器 `Payroll` 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `London` 執行個體建立特定連接，並查詢 `AdventureWorks2012.HumanResources.Employee` 資料表。 (使用 SQLNCLI 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會重新導向至最新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者)。  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 下列範例會建立與 1997 - 2003 格式之 Excel 試算表的特定連接。  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  

