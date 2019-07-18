---
title: 安裝 SCOM 管理組件-Analytics Platform System |Microsoft Docs
description: 請遵循下列步驟來下載並安裝適用於 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理組件。 監視 SQL Server PDW 的 SCOM 所需的管理組件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ac213e71d3754ccf610ba5c0874cea32c3737760
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960813"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>針對分析平台系統安裝 SQL Server Operations Manager (SCOM) 管理組件
請遵循下列步驟來下載並安裝適用於 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理組件。 監視 SQL Server PDW 的 SCOM 所需的管理組件。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 必須安裝且正在執行。 SQL Server PDW 2012 需要 System Center Operations Manager 2007 R2、 System Center Operations Manager 2012 或 System Center Operations Manager 2012 service pack 1。  
  
## <a name="Step1"></a>步驟 1:下載管理組件  
APS PDW 工作負載中，下載[Microsoft Analytics Platform System 的 System Center 管理組件](https://go.microsoft.com/fwlink/?LinkId=396857)。  
  
設備管理、 下載[SQL Server 應用裝置基礎管理組件](https://www.microsoft.com/download/details.aspx?displaylang=en&id=11436)。  
  
針對舊版的 PDW 不 APS 中，下載[System Center Monitoring Pack for Microsoft SQL Server 2012 平行資料倉儲應用裝置](https://go.microsoft.com/fwlink/p/?LinkId=282661)。  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>步驟 2:安裝管理組件  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>安裝 SQL Server 應用裝置的基底的管理組件  
  
1.  若要執行安裝，請按兩下下載 SQL Server 應用裝置基礎管理組件。  
  
2.  接受授權合約，然後按一下 [**下一步]** 。  
  
    ![接受授權合約](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  選取您自己的安裝資料夾，或使用預設管理組件的安裝資料夾。  
  
    ![選取安裝資料夾](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  按一下 **[安裝]** 。  
  
    ![確認安裝](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  按一下 [ **關閉**]。  
  
    ![按一下 [關閉]](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>安裝 SQL Server PDW 應用裝置的監視組件  
  
1.  若要執行安裝，請按兩下已下載 SQL Server PDW 應用裝置的管理組件。  
  
2.  接受授權合約，然後按一下 [**下一步]** 。  
  
    ![接受授權合約](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  選擇目錄中會包含已解壓縮的檔案。 預設會顯示預設管理組件的安裝資料夾。 選取預設值，或選取您自己的安裝資料夾。  
  
    ![選取安裝資料夾](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  按一下 **[安裝]** 。  
  
    ![確認安裝](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  按一下 [ **關閉**]。  
  
    ![安裝完成](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>下一個步驟  
既然您已安裝的管理組件，請繼續下一個步驟：[匯入適用於 PDW 的 SCOM 管理組件&#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
