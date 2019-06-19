---
title: 選取封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8cc976451c29c6d0b1656fec456b2a46b1f4f5f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727477"
---
# <a name="select-a-package"></a>選取封裝

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 **[選取封裝]** 對話方塊，即可指定訊息佇列工作可以接收訊息的來源封裝。  
  
## <a name="static-options"></a>靜態選項  
 **位置**  
 指定封裝的位置。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的位置。 選取此值會顯示動態選項 **[伺服器]** 、 **[使用 Windows 驗證]** 、 **[使用 SQL Server 驗證]** 、 **[使用者名稱]** 和 **[密碼]** 。|  
|DTSX 檔案|設定 DTSX 檔案的位置。 選取此值會顯示動態選項 **[檔案名稱]** 。|  
  
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
 **檔案名稱**  
 提供封裝的路徑，或按一下瀏覽按鈕 ([...])  並尋找封裝。  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](../../integration-services/control-flow/message-queue-task.md)  
  
  
