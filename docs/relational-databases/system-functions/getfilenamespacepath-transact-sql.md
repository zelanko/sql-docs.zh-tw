---
title: GetFileNamespacePath (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a31ca80ae50906f0789fdfef20fbf4fede9beea8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回 FileTable 中檔案或目錄的 UNC 路徑。  
  
## <a name="syntax"></a>語法  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>引數  
 *column-name*  
 Varbinary （max） 資料行名稱**file_stream** FileTable 中的資料行。  
  
 *資料行名稱*值必須是有效的資料行名稱。 它不可以是運算式，或是從其他資料類型之資料行轉換或轉型的值。  
  
 *is_full_path*  
 指定傳回相對路徑或絕對路徑的整數運算式。 *is_full_path*可以有下列值之一：  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|傳回資料庫層級目錄內的相對路徑。<br /><br /> 這是預設值。|  
|**1**|傳回以 `\\computer_name` 開始的完整 UNC 路徑。|  
  
 *@option*  
 定義路徑之伺服器元件格式化方式的整數運算式。 *@option* 可以有下列值之一：  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|傳回轉換成 NetBIOS 格式的伺服器名稱，例如：<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> 這是預設值。|  
|**1**|在不轉換的情況下傳回伺服器名稱，例如：<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|傳回完整伺服器路徑，例如：<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>傳回類型  
 **nvarchar(max)**  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在容錯移轉叢集中叢集化，則當做此路徑一部分傳回的電腦名稱是叢集執行個體的虛擬主機名稱。  
  
 當資料庫屬於 Alwayson 可用性群組，然後在**FileTableRootPath**函式會傳回虛擬網路名稱 (VNN) 而非電腦名稱。  
  
## <a name="general-remarks"></a>一般備註  
 路徑的**GetFileNamespacePath**函式會傳回邏輯目錄或檔案路徑格式如下：  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 這個邏輯路徑不會直接對應到實體 NTFS 路徑。 FILESTREAM 的檔案系統篩選驅動程式和 FILESTREAM 代理程式會將它轉譯成實體路徑。 邏輯路徑與實體路徑之間的這個分隔可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新組織內部資料，而不會影響路徑的有效性。  
  
## <a name="best-practices"></a>最佳作法  
 若要讓程式碼和應用程式獨立於目前的電腦和資料庫之外，請避免撰寫依賴絕對檔案路徑的程式碼。 相反地，使用取得的檔案在執行階段的完整路徑**FileTableRootPath**和**GetFileNamespacePath**函式在一起，如下列範例所示。 根據預設， **GetFileNamespacePath** 函數會傳回資料庫根路徑之下的檔案相對路徑。  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
 下列範例示範如何呼叫**GetFileNamespacePath**函式可取得檔案或目錄在 FileTable 中的 UNC 路徑。  
  
```  
-- returns the relative path of the form “\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
  
-- returns “\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 FileTables 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
