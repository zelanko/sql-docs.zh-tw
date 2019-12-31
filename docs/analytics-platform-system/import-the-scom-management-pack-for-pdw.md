---
title: 匯入 SCOM 管理元件
description: 請遵循下列步驟來匯入適用于分析平臺系統（AP）的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視平行資料倉儲。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401087"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>匯入 SCOM 管理元件-Analytics Platform System
請遵循下列步驟來匯入適用于分析平臺系統（AP）的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視平行資料倉儲。 
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝管理元件。 請參閱[安裝 SCOM 管理元件 &#40;分析平臺系統&#41;](install-the-scom-management-packs.md)。  
  
## <a name="Step1"></a>步驟1：匯入 SQL Server 設備基礎管理元件  
  
1.  以 Operations Manager 2007 管理群組的 Operations Manager 管理員角色成員帳戶登入電腦。  
  
2.  在 Operations 主控台中，按一下 [系統管理]****。  
  
3.  在 [**管理元件**] 節點上按一下滑鼠右鍵，然後按一下 [匯**入管理元件**]。  
  
    ![按一下 [匯入管理組件]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理元件清單中，選取您要匯入的管理元件，按一下 [**選取**]，然後按一下 [**新增**]。  
  
    ![管理元件清單](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜尋**設備**，然後向下切入至 SQL Server 應用裝置]，然後按一下 [**新增**這兩個選項]。  
  
    ![SQL Server 應用裝置基礎](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  在選取的底部窗格中有兩個管理元件，然後按一下 **[確定**]。  
  
    ![選取這兩個管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  按一下 **[安裝]**。  
  
    ![按一下 [安裝]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成後，按一下 [**關閉**]。  
  
    ![完成時，請按一下 [關閉]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>匯入 Microsoft SQL Server 2008 R2 平行處理資料倉儲設備的監視元件  
  
1.  在 [**管理元件**] 節點上按一下滑鼠右鍵，然後按一下 [匯**入管理元件**]。  
  
2.  選擇 [**從磁片加入**]。  
  
    ![以滑鼠右鍵按一下 [管理組件]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  移至您解壓縮 SQL Server PDW 管理元件的位置，然後選擇 [要匯入的管理元件] 區段中的三個管理元件。 若要這麼做，您可以選取第一個，按一下 [Shift]，然後選取最後一個。 全部選取之後，請按一下 [**開啟**]。  
  
    ![選取管理元件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  按一下 **[安裝]**。  
  
    ![按一下 [安裝]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  按一下 **關閉**。  
  
    ![按一下 [關閉]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>後續步驟  
現在您已匯入管理元件，請繼續進行下一個步驟：[設定 SCOM 以監視分析平臺系統 &#40;分析平臺系統&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
