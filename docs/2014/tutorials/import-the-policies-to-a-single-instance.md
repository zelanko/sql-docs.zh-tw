---
title: 將原則匯入的單一執行個體 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 410f3a317a9d3ad2f8cab52d9f57fd4a63c1c36c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62865097"
---
# <a name="import-the-policies-to-a-single-instance"></a>將原則匯入至單一執行個體
  在這項工作中，您將會針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的單一執行個體，匯入您要排程到以原則為基礎之管理的最佳作法原則。  
  
## <a name="prerequisites"></a>先決條件  
 您必須在執行 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更新版本的伺服器上執行此程序。  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>匯入 Database Engine 的最佳做法原則  
  
1.  啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，然後連接至 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在 [物件總管] 中，展開**管理**，然後展開**原則管理**。  
  
3.  以滑鼠右鍵按一下**原則**，然後按一下**匯入原則**。  
  
4.  在 [**匯入**] 對話方塊中的 [下一步**要匯入檔案**方塊中，按一下省略符號 ( **...** )] 按鈕。  
  
5.  在 **查看**清單中，瀏覽至下列資料夾，其中包含最佳作法原則：  
  
     **C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  檔案路徑可能會隨著您安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程式檔案的位置、執行 32 位元或 64 位元作業系統，以及語言識別碼而有所不同。  
  
6.  在 **選取原則**對話方塊中，選取一或多個原則的檔案。  
  
     若要選取非相鄰的檔案，按一下某個檔案、按住 CTRL 鍵，然後按一下其他各個檔案。 若要選取相鄰的檔案，按一下順序中的第一個檔案、按住 SHIFT 鍵，然後按一下最後一個檔案。  
  
7.  當您完成選取的檔案，請按一下**開啟**。  
  
8.  在 **匯入**對話方塊方塊中，請確定**原則狀態**清單設定為**匯入時保留原則狀態**（預設值），然後按一下  **確定**.  
  
     匯入原則**原則**下方的節點**原則管理**。 根據預設，匯入的原則會設為「視需要」評估模式。  
  
## <a name="next-steps"></a>後續步驟  
 [排程原則](../../2014/tutorials/schedule-the-policies.md)  
  
  
