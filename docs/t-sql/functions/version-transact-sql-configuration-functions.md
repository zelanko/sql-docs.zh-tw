---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1894f0e4aa31e8b80255fb49f30c7cfe1c1a146b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67927536"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;Version - Transact SQL Configuration Functions
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回系統和建立資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目前安裝的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>傳回型別  
 **nvarchar**  
  
## <a name="remarks"></a>備註  
 @@VERSION 結果會以一個 nvarchar 字串表示。 您可以使用 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) 函式來擷取個別的屬性值。  
  
 傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的下列資訊。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本  
  
-   處理器架構  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建置日期  
  
-   著作權聲明  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本  
  
-   作業系統版本  
  
 傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 的下列資訊。  
  
-   版本 - "Microsoft SQL Azure"  
  
-   產品層級 - "(RTM)"  
  
-   產品版本  
  
-   建置日期  
  
-   著作權聲明  

> [!NOTE]  
> 我們了解由 @@VERSION 所回報的產品版本對於 Azure SQL Database 而言並不正確的問題。 Azure SQL Database 所執行的 SQL Server 資料庫引擎之版本，一定會領先於 SQL Server 的內部部署版本，且會包含最新的安全性修正。 這表示修補程式等級一律會與 SQL Server 的內部部署版本對等或領先，且在 SQL Server 中提供的最新功能，在 Azure SQL Database 中也會提供。
>
> 若要以程式設計方式判斷引擎版本，請使用 SELECT SERVERPROPERTY('EngineEdition')。 此查詢將針對單一資料庫/彈性集區傳回 '5'，並針對 Azure SQL Database 中的受控執行個體傳回 '8'。 
>
> 解決此問題之後，將會更新文件。

  
## <a name="examples"></a>範例  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>A：傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目前版本  
 下列範例會顯示傳回目前安裝架構的版本資訊。  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. 傳回 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 的目前版本  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>另請參閱  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

