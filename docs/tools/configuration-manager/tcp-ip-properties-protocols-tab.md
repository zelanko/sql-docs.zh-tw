---
title: TCP/IP 屬性 （通訊協定索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 038c179061c2210278dbfadea236be9dc0bcb09f
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728298"
---
# <a name="tcpip-properties-protocols-tab"></a>TCP/IP 屬性 (通訊協定索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用 [TCP/IP 屬性]  對話方塊來設定 TCP/IP 通訊協定的選項。 按一下左窗格中的 [TCP/IP]  ，在詳細資料窗格中顯示個別的 IP 位址組態。  
  
 Microsoft SQL Server 必須重新啟動之後，變更才能生效。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是]  和 [否]  。  
  
 **Keep Alive**  
 指定傳送保持運作封包以確認連接遠端是否仍然可用的間隔 (毫秒)。  
  
 **Listen All**  
 指定 SQL Server 是否將接聽電腦的網路卡所繫結的所有 IP 位址。 如果設為 [否]  ，請使用每個 IP 位址的屬性對話方塊，分別設定每個 IP 位址。 如果設為 [是]  ，[IPAll]  屬性方塊的設定將套用到所有 IP 位址。 預設值是 [是]  。  
  
 **No Delay**  
 SQL Server 未實作此屬性的變更。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Creating a Valid Connection String Using TCP IP](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
