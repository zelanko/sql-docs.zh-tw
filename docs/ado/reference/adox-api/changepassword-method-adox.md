---
title: ChangePassword 方法（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de8baf504a76407037322fd6b799f6d63584eae7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967033"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
變更[使用者](../../../ado/reference/adox-api/user-object-adox.md)帳戶的密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>參數  
 *OldPassword*  
 指定使用者現有密碼的**字串**值。 如果使用者目前沒有密碼，請使用空字串（""）進行*OldPassword*。  
  
 *NewPassword*  
 指定新密碼的**字串**值。  
  
## <a name="remarks"></a>備註  
 基於安全性理由，除了新密碼之外，還必須指定舊密碼。  
  
 如果提供者不支援受信任者屬性的管理，將會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 和 Users Append、ChangePassword 方法範例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
