---
title: 代理程式設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.perfprofiles.f1
helpviewer_keywords:
- Agent Profiles dialog box
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0d31b6cff8b4e0f1845ddb9c5e0fd3a24fc24e4e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288304"
---
# <a name="agent-profiles"></a>代理程式設定檔
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  使用 **[代理程式設定檔]** 對話方塊，即可管理代理程式設定檔。 代理程式設定檔提供便於管理每一個代理程式執行階段參數的方式。 每一個代理程式都有預設的設定檔，有些代理程式還有其他預先定義的設定檔。 例如，合併代理程式有專為低頻寬連接設計的「慢速連結」設定檔。 預先定義的設定檔對大部份應用程式而言已經足夠，但您也可以建立使用者自訂設定檔，來自訂代理程式的行為。  
  
## <a name="options"></a>選項。  
 **選取頁面**  
 在左窗格中選取代理程式，右窗格就會顯示代理程式的設定檔。  
  
 **新項目的預設值**  
 選取為指定類型之代理程式建立作業時所使用的設定檔。 例如，若您對合併式發行集建立一些訂閱，則每一個訂閱的合併代理程式作業就會使用所選取的設定檔。 如果您要變更現有作業的設定檔，請選取設定檔，然後按一下 **[變更現有的代理程式]** 。  
  
 **名稱**  
 設定檔的名稱。  
  
 **型別**  
 設定檔的類型： **[使用者]** (使用者自訂) 或 **[系統]** (預先定義)。  
  
 **屬性 (...)**  
 按一下即可檢視代理程式設定檔中，每一個參數所使用的值。  
  
 **新增**  
 按一下即可建立新的設定檔。  
  
 **刪除**  
 選取使用者自訂設定檔，然後按一下 **[刪除]** 即可刪除該設定檔。 預先定義的設定檔無法刪除。  
  
 **[變更現有的代理程式]**  
 選取設定檔，然後按一下 **[變更現有的代理程式]** ，即可指定特定代理程式類型的所有現有作業，都使用選取的設定檔。 例如，若您對合併式發行集建立了一些訂閱，但您要變更設定檔，以指定每個訂閱的合併代理程式作業都使用 **[慢速連結代理程式設定檔]** ，請選取該設定檔，然後按一下 **[變更現有的代理程式]** 。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
