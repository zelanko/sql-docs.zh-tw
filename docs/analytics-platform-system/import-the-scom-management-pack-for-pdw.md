---
title: 匯入 SCOM 管理元件
description: 請遵循下列步驟，將適用于 Analytics Platform System (AP) 的 System Center Operations Manager (SCOM) 管理元件匯入。 需要有管理元件，才能從 SCOM 監視平行資料倉儲。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 770359a9ddb04eb8aaf45af7dd5b95447c30f264
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523865"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>匯入 SCOM 管理套件-分析平臺系統
請遵循下列步驟，將適用于 Analytics Platform System (AP) 的 System Center Operations Manager (SCOM) 管理元件匯入。 需要有管理元件，才能從 SCOM 監視平行資料倉儲。 
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>開始之前  
**先決條件**  
  
必須安裝並執行 System Center Operations Manager 2007 R2。  
  
必須安裝管理元件。 請參閱 [&#40;Analytics Platform System&#41;安裝 SCOM 管理套件 ](install-the-scom-management-packs.md)。  
  
## <a name="step-1-import-the-sql-server-appliance-base-management-pack"></a><a name="Step1"></a>步驟1：匯入 SQL Server 設備基礎管理套件  
  
1.  以 Operations Manager 2007 管理群組的 Operations Manager 管理員角色成員帳戶登入電腦。  
  
2.  在 Operations 主控台中，按一下 [系統管理]  。  
  
3.  在 [管理組件] **** 節點上按一下滑鼠右鍵，然後按一下 [匯入管理組件] ****。  
  
    ![按一下 [匯入管理組件]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理組件清單中，選取您要匯入的管理組件、按一下 [選取]****，然後按一下 [新增]****。  
  
    ![管理元件清單](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜尋 **設備** ，然後向下切入 SQL Server 設備基礎，然後按一下 [ **新增** 兩個選項]。  
  
    ![SQL Server 應用裝置基礎](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  當兩個管理元件在底部選取的窗格中，然後按一下 **[確定**]。  
  
    ![選取這兩個管理組件](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  按一下 [Install]  。  
  
    ![螢幕擷取畫面，顯示 [選取管理元件] 步驟上的 [匯入管理元件] 步驟，其中的 [安裝] 選項以紅色圈起。](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成之後，按一下 [ **關閉**]。  
  
    ![完成時，請按一下 [關閉]](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="import-the-monitoring-pack-for-microsoft-sql-server-2008-r2-parallel-data-warehouse-appliance"></a><a name="Step2"></a>匯入 Microsoft SQL Server 2008 R2 平行資料倉儲設備的監視元件  
  
1.  在 [管理組件] **** 節點上按一下滑鼠右鍵，然後按一下 [匯入管理組件] ****。  
  
2.  選擇 [ **從磁片加入**]。  
  
    ![以滑鼠右鍵按一下 [管理組件]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  移至您解壓縮 SQL Server PDW 管理元件的位置，然後選擇 [選取要匯入的管理元件] 區段中的三個管理元件。 若要這麼做，您可以選取第一個，然後按一下 [Shift]，再選取最後一個。 全部選取之後，按一下 [ **開啟**]。  
  
    ![選取管理元件](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  按一下 [Install]  。  
  
    ![[選取管理元件] 步驟上的 [匯入管理元件] 步驟的另一個螢幕擷取畫面，其中以紅色圈起的安裝選項。](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  按一下 [關閉]。  
  
    ![按一下 [關閉]](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>後續步驟  
現在您已匯入管理元件，請繼續進行下一個步驟： [設定 SCOM 以監視 Analytics Platform system &#40;Analytics Platform system&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
