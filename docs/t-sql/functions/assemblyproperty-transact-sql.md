---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f71e88a63a3f3518ba983f494b69b4046346a5e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658146"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函數傳回組件屬性的相關資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>引數  
*assembly_name*  
組件的名稱。
  
*property_name*  
針對要擷取相關資訊的屬性，此屬性的名稱。 *property_name* 可為以下其中一個值：
  
|ReplTest1|Description|  
|---|---|
|**CultureInfo**|組件的地區設定。|  
|**PublicKey**|組件的公開金鑰或公開金鑰 Token。|  
|**MvID**|由編譯器產生的完整組件版本識別碼。|  
|**VersionMajor**|組件之四部份版本識別碼的主要元件 (第一部份)。|  
|**VersionMinor**|組件之四部份版本識別碼的次要元件 (第二部份)。|  
|**VersionBuild**|組件之四部份版本識別碼的建置元件 (第三部份)。|  
|**VersionRevision**|組件之四部份版本識別碼的修訂元件 (第四部份)。|  
|**SimpleName**|組件的簡單名稱。|  
|**架構**|組件的處理器架構。|  
|**CLRName**|將簡單名稱、版本號碼、文化、公開金鑰和組件架構加以編碼的標準字串。 這個值可以唯一識別 Common Language Runtime (CLR) 端的組件。|  
  
## <a name="return-type"></a>傳回類型
**sql_variant**
  
## <a name="examples"></a>範例  
下列範例假設 `HelloWorld` 組件是已在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中註冊的組件。 如需詳細資訊，請參閱 [Hello World 範例](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>另請參閱
[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
