---
title: 選取封裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 931a122e188f157a2fbcf32adbf9c6dc420d11f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029851"
---
# <a name="select-a-package"></a>選取封裝
  使用 **[選取封裝]** 對話方塊，即可指定訊息佇列工作可以接收訊息的來源封裝。  
  
## <a name="static-options"></a>靜態選項  
 **位置**  
 指定封裝的位置。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的位置。 選取此值會顯示動態選項 **[伺服器]**、 **[使用 Windows 驗證]**、 **[使用 SQL Server 驗證]**、 **[使用者名稱]** 和 **[密碼]**。|  
|DTSX 檔案|設定 DTSX 檔案的位置。 選取此值會顯示動態選項 **[檔案名稱]**。|  
  
## <a name="location-dynamic-options"></a>位置動態選項  
  
### <a name="location--sql-server"></a>位置 = SQL Server  
 **封裝名稱**  
 選取儲存在指定之伺服器上的封裝。  
  
 **[伺服器]**  
 提供伺服器名稱或從清單中選取伺服器。  
  
 **[使用 Windows 驗證]**  
 按一下即可使用 Windows 驗證。  
  
 **[使用 SQL Server 驗證]**  
 按一下即可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 **[使用者名稱]**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供登入伺服器時要使用的使用者名稱。  
  
 **[密碼]**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供密碼。  
  
### <a name="location--dtsx-file"></a>位置 = DTSX 檔案  
 **[檔案名稱]**  
 提供封裝的路徑，或按一下瀏覽按鈕 **(...)** 並尋找封裝。  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](message-queue-task.md)  
  
  