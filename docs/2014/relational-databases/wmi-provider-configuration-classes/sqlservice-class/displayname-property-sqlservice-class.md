---
title: DisplayName 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- DisplayName Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5438ccd554023f6a942f56b81d1c0ec0d9120bec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124558"
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 屬性 (SqlService 類別)
  取得服務的顯示名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.DisplayName [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定此服務之顯示名稱的字串值。  
  
## <a name="remarks"></a>備註  
 這個字串的最大長度為 256 個字元。 此名稱在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員中有保留大小寫。 不過，顯示名稱比較一定不區分大小寫。  
  
## <a name="example"></a>範例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
