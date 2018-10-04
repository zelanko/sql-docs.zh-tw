---
title: ChangePassword 方法 (ADOX) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 96268fac4b81230fcb63db6b48ef4ef794abb9c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788706"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
變更的密碼[使用者](../../../ado/reference/adox-api/user-object-adox.md)帳戶。  
  
## <a name="syntax"></a>語法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>參數  
 *OldPassword*  
 A**字串**值，指定使用者的現有密碼。 如果使用者目前不需要密碼，使用空字串 ("") 的*OldPassword*。  
  
 *NewPassword*  
 A**字串**值，指定新的密碼。  
  
## <a name="remarks"></a>備註  
 基於安全性理由，您必須指定舊密碼，除了新的密碼。  
  
 如果提供者不支援 trustee 屬性的系統管理，就會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 和 Users Append、ChangePassword 方法範例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
