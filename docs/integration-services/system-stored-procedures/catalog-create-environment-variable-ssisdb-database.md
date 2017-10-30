---
title: "catalog.create_environment_variable （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5636651cccbb43c6c1627d1f28eccd9b3f9b5b0d
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立環境變數。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>引數  
 [@folder_name =] *folder_name*  
 包含環境之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [@environment_name =] *environment_name*  
 環境的名稱。 *Environment_name*是**nvarchar （128)**。  
  
 [@variable_name =] *variable_name*  
 環境變數的名稱。 *Variable_name*是**nvarchar （128)**。  
  
 [@data_type =] *data_type*  
 變數的資料類型。 支援的環境變數資料類型包括**布林**，**位元組**， **DateTime**， **Double**， **Int16**， **Int32**， **Int64**，**單一**，**字串**， **UInt32**，和**UInt64**。 不支援的環境變數資料類型包括**Char**， **DBNull**，**物件**，和**Sbyte**。 資料型別*data_type*參數是**nvarchar （128)**。  
  
 [@sensitive =]*機密*  
 指出變數是否包含機密值。 使用 `1` 值表示環境變數的值是機密值，或者，使用 `0` 值則表示該值不是機密值。 機密值會在儲存時加密。 機密值則不會儲存為純文字。*機密*是**元**。  
  
 [@value =]*值*  
 環境變數的值。 *值*是**sql_variant**。  
  
 [@description =]*描述*  
 環境變數的描述。 *值*是**nvarchar （1024)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   環境的 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱、環境名稱或環境變數名稱無效  
  
-   變數名稱已經存在於環境中  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
 環境變數可以用來將值有效地指派給專案參數或封裝參數，以用於封裝的執行中。 環境變數啟用了參數值的組織。 變數名稱在環境中必須是唯一的。  
  
 預存程序會驗證變數的資料類型，以確定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄可支援該變數。  
  
> [!TIP]  
>  請考慮使用**Int16**中的資料類型[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]而不是不支援**Sbyte**資料型別。  
  
 值傳遞給這個預存程序*值*參數會從轉換[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]根據下表的資料類型：  
  
|Integration Services 資料類型|SQL Server 資料類型|  
|------------------------------------|--------------------------|  
|**布林**|**bit**|  
|**位元組**|**二進位**， **varbinary**|  
|**DateTime**|**datetime**， **datetime2**， **datetimeoffset**， **smalldatetime**|  
|**Double**|精確數值：**十進位**，**數值**;近似數值： **float**，**真實**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|精確數值：**十進位**，**數值**;近似數值： **float**，**真實**|  
|**字串**|**varchar**， **nvarchar**， **char**|  
|**UInt32**|**int** (**int**是最接近可用對應**Uint32**。)|  
|**UInt64**|**bigint** (**int**是最接近可用對應**Uint64**。)|  
  
  

