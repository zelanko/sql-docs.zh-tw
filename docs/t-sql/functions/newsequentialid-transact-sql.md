---
title: NEWSEQUENTIALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- NEWSEQUENTIALID
- NEWSEQUENTIALID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEWSEQUENTIALID function
- GUIDs [SQL Server]
ms.assetid: e06d2cab-f1ff-42f1-8550-6aaec57be36f
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7766d91cfe3b72ff2edbca9d5719a00d1ea63217
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053365"
---
# <a name="newsequentialid-transact-sql"></a>NEWSEQUENTIALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立一個 GUID，該 GUID 會大於這個函數先前在指定的電腦啟動 Windows 後所產生的任何 GUID。 重新啟動 Windows 後，GUID 可以從較低的範圍再次啟動，但仍是全域唯一的。 將 GUID 資料行當做資料列識別碼使用時，使用 NEWSEQUENTIALID 可能比使用 NEWID 函數更快。 這是因為 NEWID 函數會造成隨機活動，因此會使用較少的快取資料頁面。 使用 NEWSEQUENTIALID 也有助於完全填滿資料與索引頁面。  
  
> [!IMPORTANT]  
>  如果您有隱私權顧慮，請勿使用這個函數。 因為使用者不難猜出下一個產生的 GUID 值，進而存取與該 GUID 相關聯的資料。  
  
 NEWSEQUENTIALID 是 Windows [UuidCreateSequential](http://go.microsoft.com/fwlink/?LinkId=164027) 函式上的一個包裝函式，其[套用了一些隨機位元組](https://blogs.msdn.microsoft.com/dbrowne/2012/07/03/how-to-generate-sequential-guids-for-sql-server-in-net/)。
  
> [!WARNING]  
>  UuidCreateSequential 函式有硬體相依性。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上，當資料庫 (例如自主資料庫) 移動到另一部電腦時，順序值的叢集便可進行開發。 使用 Always On 和在 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 上時，若資料庫容錯移轉至不同的電腦，順序值的叢集便可進行開發。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
NEWSEQUENTIALID ( )  
```  
  
## <a name="return-type"></a>傳回類型  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Remarks  
 NEWSEQUENTIALID() 只能搭配使用 **uniqueidentifier** 類型之資料表資料行的 DEFAULT 條件約束。 例如：  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT NEWSEQUENTIALID());   
```  
  
 當 NEWSEQUENTIALID() 用於 DEFAULT 運算式時，不能與其他純量運算子結合。 例如，您不可以執行下列作業：  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT dbo.myfunction(NEWSEQUENTIALID()));  
```  
  
 在上一個範例中，`myfunction()` 是一個純量使用者自訂的純量函數，可以接受和傳回 `uniqueidentifier` 值。  
  
 NEWSEQUENTIALID 無法於查詢中參考。  
  
 您可以使用 NEWSEQUENTIALID 來產生 GUID，以減少在索引分葉層級的網頁競爭。  
  
 使用 NEWSEQUENTIALID 所產生的 GUID 在該電腦上都是唯一的。 唯有在來源電腦具有網路卡時，使用 NEWSEQUENTIALID 所產生的 GUID 在多部電腦上才是唯一的。  
  
## <a name="see-also"></a>另請參閱  
 [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)   
 [比較運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
