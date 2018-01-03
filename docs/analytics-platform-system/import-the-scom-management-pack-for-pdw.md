---
title: "匯入 PDW (Analytics Platform System) 的 SCOM 管理組件"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa735041-8e58-4886-ae3b-36f3c6298b12
caps.latest.revision: "6"
ms.openlocfilehash: 179395b7befdf934fcc44532944f4b535b9d3c5a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="import-the-scom-management-pack-for-pdw"></a>匯入 PDW 的 SCOM 管理組件
依照下列步驟，針對 SQL Server PDW 匯入 System Center Operations Manager (SCOM) 管理組件。 監視 SQL Server PDW 從 SCOM 所需的管理組件。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝管理組件。 請參閱[SCOM 管理組件 &#40; 安裝Analytics Platform System &#41;](install-the-scom-management-packs.md).  
  
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
現在您已匯入管理組件，繼續下一個步驟：[設定 SCOM 監視 Analytics Platform System &#40;Analytics Platform System &#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
