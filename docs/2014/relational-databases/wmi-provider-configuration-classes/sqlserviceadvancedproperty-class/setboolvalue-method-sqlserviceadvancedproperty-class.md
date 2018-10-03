---
title: 設定中斷點 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9269cd8d4e01257f4af2642ad767353d09444a6e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130332"
---
# <a name="set-breakpoints"></a>[設定中斷點]
  使用 **[設定中斷點]** 對話方塊，即可指定要啟用中斷點的事件並控制中斷點的行為。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 選取即可在事件上啟用中斷點。  
  
 **中斷條件**  
 檢視要設定中斷點之可用事件的清單。  
  
 **叫用計數類型**  
 指定中斷點生效的時間。  
  
|值|描述|  
|-----------|-----------------|  
|**永遠**|叫用中斷點時，一律暫停執行。|  
|**叫用計數等於**|當中斷點發生的次數等於叫用計數時，暫停執行。|  
|**叫用大於或等於**|當中斷點發生的次數大於或等於叫用計數時，暫停執行。|  
|**叫用計數倍數**|每當到達叫用計數的倍數時，暫停執行。 例如，若您將此選項設定為 5，則每到達五次叫用便會暫停執行。|  
  
 **叫用計數**  
 指定觸發中斷的叫用次數。 如果中斷點永遠有效，則無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [偵錯控制流程](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
