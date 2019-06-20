---
title: 匯入 SCOM 管理組件-Analytics Platform System |Microsoft Docs
description: 請遵循下列步驟來匯入 System Center Operations Manager (SCOM) 管理組件的 Analytics Platform System (APS)。 監視從 SCOM 的平行處理資料倉儲時，所需的管理組件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c4280fb257147f3c401badc6eaec18929f6d69b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149635"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>匯入 SCOM 管理組件-Analytics Platform System
請遵循下列步驟來匯入 System Center Operations Manager (SCOM) 管理組件的 Analytics Platform System (APS)。 監視從 SCOM 的平行處理資料倉儲時，所需的管理組件。 
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝管理組件。 請參閱[安裝的 SCOM 管理組件&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)。  
  
## <a name="Step1"></a>步驟 1:匯入 SQL Server 應用裝置的基底的管理組件  
  
1.  登入帳戶是 Operations Manager 2007 管理群組的 Operations Manager 系統管理員角色的成員電腦。  
  
2.  在 Operations 主控台中，按一下**管理**。  
  
3.  以滑鼠右鍵按一下**管理組件**節點，然後再按一下**匯入管理組件**。  
  
    ![按一下 匯入管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理組件清單中，選取您想要匯入，請按一下 管理組件**選取** ，然後按一下**新增**。  
  
    ![管理組件清單](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜尋**設備**然後向下切入至 SQL Server 應用裝置基底，然後按一下 **新增**兩個選擇。  
  
    ![SQL Server 應用裝置基底](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  後兩個管理組件已在下方選取窗格中，按一下 **確定**。  
  
    ![選取這兩個管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  按一下 **[安裝]** 。  
  
    ![按一下 [安裝]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成後，按一下**關閉**。  
  
    ![完成後，按一下 關閉](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>匯入監視組件，如 Microsoft SQL Server 2008 R2 平行資料倉儲應用裝置  
  
1.  以滑鼠右鍵按一下**管理組件**節點，然後再按一下**匯入管理組件**。  
  
2.  選擇**從磁碟加入**...  
  
    ![以滑鼠右鍵按一下 管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  移至您解壓縮 SQL Server PDW 管理組件的位置，然後選擇 「 選取管理組件匯入 」 一節中的三個管理組件。 選取第一個、 按一下 shift 鍵，然後選取最後一個，您可以執行這項操作。 一旦它們全部選取，按一下**開啟**。  
  
    ![選取管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  按一下 **[安裝]** 。  
  
    ![按一下 [安裝]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  按一下 [ **關閉**]。  
  
    ![按一下 [關閉]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>下一個步驟  
既然您已匯入管理組件，請繼續下一個步驟：[設定 SCOM 以監視 Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
