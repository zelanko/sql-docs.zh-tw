---
title: 安裝 SCOM 管理元件
description: 請遵循下列步驟來下載並安裝適用于 SQL Server PDW 的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視 SQL Server PDW。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3652b767f4628b61f5dd363999838418ff933aa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401076"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>安裝適用于 Analytics Platform System 的 SQL Server Operations Manager （SCOM）管理元件
請遵循下列步驟來下載並安裝適用于 SQL Server PDW 的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視 SQL Server PDW。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 必須已安裝且正在執行。 SQL Server PDW 2012 需要 System Center Operations Manager 2007 R2、System Center Operations Manager 2012 或 System Center Operations Manager 2012 Service Pack 1。  
  
## <a name="Step1"></a>步驟1：下載管理元件  
針對 [AP PDW] 工作負載，請下載[Microsoft Analytics Platform System 的 System Center 管理元件](https://go.microsoft.com/fwlink/?LinkId=396857)。  
  
針對裝置管理，請下載[SQL Server 的設備基礎管理元件](https://docs.microsoft.com/previous-versions/system-center/packs/gg602398(v=technet.10))。  
  
針對不含 AP 的舊版 PDW，請下載[適用于 Microsoft SQL Server 2012 平行處理資料倉儲設備的 System Center Monitoring Pack](https://go.microsoft.com/fwlink/p/?LinkId=282661)。  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>步驟2：安裝管理元件  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>安裝 SQL Server 設備基礎管理元件  
  
1.  若要執行安裝，請按兩下下載的 SQL Server 設備基礎管理元件。  
  
2.  接受授權合約，然後按 **[下一步]**。  
  
    ![接受授權合約](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  選取您自己的安裝資料夾，或使用預設的管理元件安裝資料夾。  
  
    ![選取安裝資料夾](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  按一下 **[安裝]**。  
  
    ![確認安裝](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  按一下 **關閉**。  
  
    ![按一下 [關閉]](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>安裝 SQL Server PDW 設備的監視元件  
  
1.  若要執行安裝，請按兩下下載的 SQL Server PDW 裝置管理元件。  
  
2.  接受授權合約，然後按 **[下一步]**。  
  
    ![接受授權合約](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  選擇要保存解壓縮檔案的目錄。 預設會顯示預設的管理元件安裝資料夾。 選取預設值，或選取您自己的安裝資料夾。  
  
    ![選取安裝資料夾](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  按一下 **[安裝]**。  
  
    ![確認安裝](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  按一下 **關閉**。  
  
    ![安裝完成](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>後續步驟  
現在您已安裝管理元件，請繼續進行下一個步驟：匯[入適用于 PDW 的 SCOM 管理元件 &#40;分析平臺系統&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
