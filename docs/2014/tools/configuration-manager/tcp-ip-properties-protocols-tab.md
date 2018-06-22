---
title: TCP-IP 內容 （通訊協定索引標籤） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 57b3bd32574aadbd42b25b626756cc20369d9b8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030916"
---
# <a name="tcp---ip-properties-protocols-tab"></a>TCP-IP 內容 （通訊協定索引標籤）
  使用 [TCP/IP 屬性] 對話方塊來設定 TCP/IP 通訊協定的選項。 按一下左窗格中的 [TCP/IP]，在詳細資料窗格中顯示個別的 IP 位址組態。  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動之後，變更才能生效。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
 **Keep Alive**  
 指定傳送保持運作封包以確認連接遠端是否仍然可用的間隔 (毫秒)。  
  
 **Listen All**  
 指定 SQL Server 是否將接聽電腦的網路卡所繫結的所有 IP 位址。 如果設為 [否]，請使用每個 IP 位址的屬性對話方塊，分別設定每個 IP 位址。 如果設為 [是]，[IPAll] 屬性方塊的設定將套用到所有 IP 位址。 預設值是 [是]。  
  
 **No Delay**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未實作此屬性的變更。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用 TCP IP 建立有效的連接字串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
  