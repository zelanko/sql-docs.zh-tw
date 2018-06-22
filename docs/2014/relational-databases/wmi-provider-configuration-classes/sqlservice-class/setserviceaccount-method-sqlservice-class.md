---
title: SetServiceAccount 方法 （SqlService 類別） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetServiceAccount Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 74f296fd52640c950d7d2c4b227a1c3aedb17df7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022572"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount 方法 (SqlService 類別)
  嘗試變更服務執行個體執行時所使用的使用者名稱和密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetServiceAccount(  
ServiceStartName , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *ServiceStartName*  
 指定此服務執行時所使用之帳戶名稱的字串值。 根據服務類型而定，此帳戶名稱可能是 DomainName\Username 的格式。 當它執行時，將會使用兩種格式的其中一種來記錄服務處理序：  
  
-   如果帳戶屬於內建網域，可以指定 \Username。  
  
-   如果指定 NULL，則服務會以登入**LocalSystem**帳戶。  
  
 核心或系統層級的驅動程式， *StartName*包含驅動程式的物件名稱，\FileSystem\Rdr 或 \Driver\Xns，I/O 系統用來載入裝置驅動程式。 如果指定了 NULL，將會根據類似 DWDOM\Admin 的服務名稱，使用 I/O 系統所建立的預設物件名稱來執行驅動程式。  
  
 *ServiceStartPassword*  
 指定的密碼中的帳戶名稱的字串值*StartName*參數。 如果您不要變更密碼，請指定 NULL。 如果此服務沒有密碼，請指定空字串。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  