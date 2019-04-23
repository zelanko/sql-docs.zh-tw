---
title: 新增使用者角色 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newrole.f1
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca926ca10a391983900402d776e075ac321dea48
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940324"
---
# <a name="new-user-role-management-studio"></a>新增使用者角色 (Management Studio)
  使用此頁面，即可建立項目層級角色定義。 項目層級角色定義是具名的工作集合，其中列舉了與資料夾、報表、模型、資源以及共用資料來源相關，且使用者可以執行的工作。 預先定義的瀏覽者角色，就是項目層級角色定義的範例，這個角色會識別報表使用者在導覽資料夾和檢視報表時，可能需要的動作種類。  
  
 預期角色定義的數目並不多。 多數組織都只需要少數的角色定義。 不過，如果預先定義的角色定義不敷使用，您可以加以改變或建立新的角色定義。  
  
> [!NOTE]  
>  角色定義只會用於以原生模式執行的報表伺服器。 如果報表伺服器是針對 SharePoint 整合所設定，這個頁面就無法使用。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入角色定義的名稱。 角色定義名稱在報表伺服器命名空間內必須是唯一的。 名稱必須至少包含一個英數字元。 它也可以包含空格和某些符號。 指定名稱時，請勿使用下列字元：  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **說明**  
 鍵入說明如何使用角色的描述，並列舉該角色支援的項目。  
  
 **工作**  
 選取可以透過此角色執行的工作。 您無法建立新工作，或修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支援的現有工作。 項目層級角色定義中只能使用項目層級工作。  
  
 **工作描述**  
 顯示工作的描述，其中列舉出工作能夠支援的作業或權限。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [角色定義](../security/role-definitions.md)  
  
  
