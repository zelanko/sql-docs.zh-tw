---
title: 設定 Windows 以接收遠端資料表複本
description: 描述如何購買和設定使用未使用的網路連接的非設備 Windows 系統，以用於平行處理資料倉儲中的遠端資料表複製功能。 Windows 系統將裝載從 SQL Server PDW 資料庫接收遠端資料表複本的 SQL Server 資料庫。 它會與設備分開購買，並聯機到設備未受歡迎的網路。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401308"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>設定外部 Windows 系統，以使用不限型的平行處理資料倉儲接收遠端資料表複本
描述如何購買和設定非設備的 Windows 系統，並使用未使用的網路連線，以用於 SQL Server PDW 中的遠端資料表複製功能。 Windows 系統將裝載從 SQL Server PDW 資料庫接收遠端資料表複本的 SQL Server 資料庫。 它會與設備分開購買，並聯機到設備未受歡迎的網路。  
  
> [!NOTE]  
> 使用遠端資料表複本時，不需要透過未完成的網路連接。 如果 Ethernet 頻寬符合您的需求，則可以透過 Ethernet 網路進行連接。  
  
本主題說明設定遠端資料表複本的其中一個設定步驟。 如需所有設定步驟的清單，請參閱[遠端資料表複本](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>開始之前  
設定外部 Windows 系統之前，您必須：  
  
1.  購買或提供將接收遠端副本的 Windows 系統。  
  
2.  將 Windows 系統機架放在控制機架中（如果有足夠的空間）或接近設備，好讓您可以將它連線到設備的網路。  
  
3.  從您的設備硬體廠商購買無法使用的纜線和不受的網路介面卡。 我們建議使用兩個埠來購買網路介面卡，以在接收匯出的資料時容錯。 建議使用兩個埠網路介面卡，但不是必要條件。  
  
## <a name="HowToWindows"></a>設定外部 Windows 系統以接收遠端資料表複本  
若要設定外部 Windows 系統，請使用下列步驟：  
  
1.  將 [未執行的網路介面卡] 安裝到您的 Windows 系統。  
  
2.  使用「不限」的纜線，將「未充分的網路介面卡」連接到控制機架中的主要未通過交換器  
  
3.  為「未設定的網路介面卡」安裝並設定適當的 Windows 驅動程式。  
  
    適用于 Windows 的不駕駛驅動程式是由 OpenFabrics 聯盟所開發，這是一家不受駕駛廠商的產業聯盟。  正確的驅動程式可能已與您的未使用介面卡一起散發。 如果不是，可以從 www.openfabrics.org 下載驅動程式。  
  
4.  設定介面卡上每個埠的 IP 位址。 SMP 系統必須使用靜態 IP 位址，從為此用途保留的位址範圍內。 根據下列參數設定第一個埠：  
  
    -   IP 網路位址： 172.16.132. x  
  
    -   IP 子網路遮罩：255.255.128。0  
  
    -   IP 主機範圍：1-254  
  
    針對具有兩個埠的未使用網路介面卡，請根據下列參數設定第二個埠：  
  
    -   IP 網路位址： 172.16.132. x  
  
    -   IP 子網路遮罩：255.255.128。0  
  
    -   IP 主機範圍：1-254  
  
5.  如果使用了兩個通訊埠介面卡，或有多個外部 Windows 系統連線到設備，請將每個系統指派給每個 IP 子網內的不同主機號。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
