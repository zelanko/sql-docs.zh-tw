---
title: 匯入 SCOM 管理組件-Analytics Platform System |Microsoft 文件
description: 請遵循下列步驟來匯入 System Center Operations Manager (SCOM) 管理組件 Analytics Platform System (AP)。 監視從 SCOM Parallel Data Warehouse 所需的管理組件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e60d87ae58b0804a0a7296f8b489df7441683c5b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>匯入 SCOM 管理組件-Analytics Platform System
請遵循下列步驟來匯入 System Center Operations Manager (SCOM) 管理組件 Analytics Platform System (AP)。 監視從 SCOM Parallel Data Warehouse 所需的管理組件。 
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝管理組件。 請參閱[安裝 SCOM 管理組件&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)。  
  
## <a name="Step1"></a>步驟 1： 匯入 SQL Server 應用裝置的基本管理組件  
  
1.  登入帳戶是 Operations Manager 2007 管理群組的 Operations Manager 系統管理員角色的成員電腦。  
  
2.  在 Operations 主控台中，按一下**管理**。  
  
3.  以滑鼠右鍵按一下**管理組件**節點，然後再按一下**匯入管理組件**。  
  
    ![按一下 匯入管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理組件清單中，選取您要匯入，請按一下 管理組件**選取**，然後按一下 **新增**。  
  
    ![管理組件清單](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜尋**應用裝置**然後向下鑽研至 SQL Server 應用裝置基底，然後按一下 **新增**兩個選擇。  
  
    ![SQL Server 應用裝置基礎](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  當兩個管理組件已在下方選取窗格時，然後按一下**確定**。  
  
    ![選取管理組件都](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  按一下 **[安裝]**。  
  
    ![按一下 安裝](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成後，按一下**關閉**。  
  
    ![完成後，按一下 關閉](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>匯入監視組件的 Microsoft SQL Server 2008 R2 平行資料倉儲應用裝置  
  
1.  以滑鼠右鍵按一下**管理組件**節點，然後再按一下**匯入管理組件**。  
  
2.  選擇**從磁碟加入**...  
  
    ![以滑鼠右鍵按一下 管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  請移至您解壓縮 SQL Server PDW 管理組件的位置，然後選擇 「 選取管理組件匯入 」 一節中的三個管理組件。 您可以選取第一個、 按一下 shift 鍵，然後選取最後一個。 一旦它們全部選取，按一下 **開啟**。  
  
    ![選取管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  按一下 **[安裝]**。  
  
    ![按一下 安裝](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  按一下 [ **關閉**]。  
  
    ![按一下 關閉](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>下一個步驟  
現在您已匯入管理組件，繼續下一個步驟：[設定 SCOM 到監視 Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
