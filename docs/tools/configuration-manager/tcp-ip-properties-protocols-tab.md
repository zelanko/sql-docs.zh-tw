---
title: "TCP/IP 屬性 （通訊協定索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 0cb8a1ffb609405f5c27ee62d3663ba2b4214d46
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# TCP/IP 屬性 (通訊協定索引標籤)
  使用 [TCP/IP 屬性] 對話方塊來設定 TCP/IP 通訊協定的選項。 按一下左窗格中的 [TCP/IP]，在詳細資料窗格中顯示個別的 IP 位址組態。  
  
 Microsoft SQL Server 必須重新啟動之後，變更才能生效。  
  
## 選項。  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
 **Keep Alive**  
 指定傳送保持運作封包以確認連接遠端是否仍然可用的間隔 (毫秒)。  
  
 **Listen All**  
 指定 SQL Server 是否將接聽電腦的網路卡所繫結的所有 IP 位址。 如果設為 [否]，請使用每個 IP 位址的屬性對話方塊，分別設定每個 IP 位址。 如果設為 [是]，[IPAll] 屬性方塊的設定將套用到所有 IP 位址。 預設值是 [是]。  
  
 **No Delay**  
 SQL Server 未實作此屬性的變更。  
  
## 另請參閱  
 [選擇網路通訊協定](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Creating a Valid Connection String Using TCP IP](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  

