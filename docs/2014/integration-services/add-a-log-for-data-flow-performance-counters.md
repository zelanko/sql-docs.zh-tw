---
title: 加入資料流程效能計數器的記錄檔 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Integration Services]
- counters [Integration Services]
- logs [Integration Services], data flow counters
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6ffdb95c84fb905fee3092f9192f0433ebb96abc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248778"
---
# <a name="add-a-log-for-data-flow-performance-counters"></a>加入資料流程效能計數器的記錄檔
  此程序描述如何加入資料流程引擎提供之效能計數器的記錄檔。  
  
> [!NOTE]  
>  如果您在執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的電腦上安裝 [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)]，然後將該電腦升級到 [!INCLUDE[firstref_longhorn](../includes/firstref-longhorn-md.md)]，則升級程序會從電腦中移除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 效能計數器。 若要還原電腦上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 效能計數器，請在修復模式中執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式。  
  
### <a name="to-add-logging-of-performance-counters"></a>若要加入效能計數器的記錄  
  
1.  在 [控制台] 中，如果使用傳統檢視，請按一下 [系統管理工具]。 如果使用類別檢視，請按一下 [效能及維護]，然後按一下 [系統管理工具]。  
  
2.  按一下 [效能]。  
  
3.  在 [效能] 對話方塊中，展開 [效能記錄檔及警示]，以滑鼠右鍵按一下 [計數器記錄檔]，然後按一下 [新記錄檔設定]。 鍵入記錄檔的名稱。 例如，輸入 **MyLog**。  
  
4.  按一下 [確定] 。  
  
5.  在 [MyLog] 對話方塊中，按一下 [加入計數器]。  
  
6.  按一下 [使用本機電腦計數器]，以記錄本機電腦上的效能計數器，或按一下 [從下列電腦選取計數器]，然後從清單選取電腦，以記錄指定之電腦上的效能計數器。  
  
7.  在 [加入計數器] 對話方塊中，選取 [效能物件] 清單中的 [SQL Server:SSIS Pipeline]。  
  
8.  若要選取效能計數器，請執行下列其中之一：  
  
    -   選取 [所有計數器]，以記錄所有效能計數器。  
  
    -   選取 [從清單選取計數器]，並選取要使用的效能計數器。  
  
9. 按一下 **[加入]**。  
  
10. 按一下 [ **關閉**]。  
  
11. 在 [MyLog] 對話方塊中，檢閱 [計數器] 清單中記錄效能計數器的清單。  
  
12. 若要加入其他計數器，請重複步驟 5 至 10。  
  
13. 按一下 [確定] 。  
  
    > [!NOTE]  
    >  您必須使用 Administrators 群組成員的本機帳戶或網域帳戶，啟動「效能記錄檔及警示」服務。  
  
## <a name="see-also"></a>另請參閱  
 [效能計數器](performance/performance-counters.md)   
 [檢視記錄事件視窗中的記錄項目](../../2014/integration-services/view-log-entries-in-the-log-events-window.md)  
  
  
