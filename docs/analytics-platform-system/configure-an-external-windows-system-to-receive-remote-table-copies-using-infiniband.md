---
title: 設定 Windows 以接收遠端資料表複本-Parallel Data Warehouse |Microsoft Docs
description: 說明如何購買並設定非應用裝置的 Windows 系統，平行處理資料倉儲之遠端資料表複製功能搭配使用 InfiniBand 網路連線。 Windows 系統將裝載 SQL Server 資料庫從 SQL Server PDW 資料庫接收遠端資料表複本。 它是分開購買應用裝置，並連接到設備的 InfiniBand 網路。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 428dc5b4edda91f60a09a52c0326f881f257b32c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961302"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>設定外部 Windows 系統以接收遠端資料表複本使用 InfiniBand-平行處理資料倉儲
說明如何購買並設定 SQL Server PDW 中的遠端資料表複製功能搭配使用 InfiniBand 網路連接非應用裝置 Windows 系統。 Windows 系統將裝載 SQL Server 資料庫從 SQL Server PDW 資料庫接收遠端資料表複本。 它是分開購買應用裝置，並連接到設備的 InfiniBand 網路。  
  
> [!NOTE]  
> 透過 InfiniBand 網路連線不需要使用遠端資料表複本。 如果乙太網路頻寬符合您的需求，可以完成透過乙太網路連線。  
  
本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[遠端資料表複製](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>開始之前  
設定外部 Windows 系統之前，您必須：  
  
1.  購買，或提供一種 Windows 系統，將會收到遠端複本。  
  
2.  上架控制項在機架中的 Windows 系統，（如果沒有足夠的空間），或關閉足以應用裝置，以便您可以將它連接到設備的 InfiniBand 網路。  
  
3.  從您的設備的硬體廠商購買 InfiniBand 纜線和 InfiniBand 網路介面卡。 建議您購買與網路介面卡的容錯功能的兩個連接埠，接收匯出的資料時。 兩個連接埠的網路介面卡建議，但並非必要。  
  
## <a name="HowToWindows"></a>設定外部 Windows 系統，以接收遠端資料表複本  
若要設定外部 Windows 系統，請使用下列步驟：  
  
1.  安裝到您的 Windows 系統的 InfiniBand 網路介面卡。  
  
2.  連接到主要 InfiniBand 交換器使用 InfiniBand 纜線的控制機架中的 InfiniBand 網路介面卡。  
  
3.  安裝並設定適當的 Windows 驅動程式的 InfiniBand 網路介面卡。  
  
    Windows 的 InfiniBand 驅動程式開發的 OpenFabrics Alliance InfiniBand 廠商同業協會。  正確的驅動程式可能分散 InfiniBand 介面卡。 如果沒有，您可以從 www.openfabrics.org 下載驅動程式。  
  
4.  在介面卡上設定的 IP 位址，每個連接埠。 SMP 系統，才能從保留的位址範圍的靜態 IP 位址用於此用途。 設定第一個連接埠，根據下列參數：  
  
    -   IP 網路位址：172.16.132.x  
  
    -   IP 子網路遮罩：255.255.128.0  
  
    -   IP 主機範圍：1-254  
  
    InfiniBand 網路介面卡與兩個連接埠，設定第二個連接埠根據下列參數：  
  
    -   IP 網路位址：172.16.132.x  
  
    -   IP 子網路遮罩：255.255.128.0  
  
    -   IP 主機範圍：1-254  
  
5.  如果使用的兩個連接埠介面卡時，或多個外部 Windows 系統的連線至應用裝置，指派不同的主機數目，每個 IP 子網路內的每個系統。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
