---
title: 設定追蹤檔案的檔案大小上限 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- size [SQL Server], trace files
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0bb761cf3402080842ae0eaff7b04a0f312a3a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267319"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>設定追蹤檔案的檔案大小上限 (SQL Server Profiler)
  使用下列程序，可設定追蹤檔案的檔案大小上限。  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>若要設定追蹤檔的大小上限  
  
1.  在 [檔案]  功能表上按一下 [新增追蹤]  ，然後連接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]** 對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]  ，將不會顯示 [追蹤屬性]  對話方塊，而是開始追蹤。 於 [工具]  功能表，按一下 [選項]  ，並清除 [連接後立即啟動追蹤]  核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 [範本名稱]  清單中，選取追蹤範本。  
  
4.  選取 [儲存至檔案]  ，然後指定要儲存追蹤資訊的檔案。  
  
5.  在 [設定最大檔案大小]  核取方塊中，指定追蹤的檔案大小上限。 當檔案的大小到達此上限時，此檔案中便不再記錄追蹤事件。 如果選取 [啟用檔案換用]  (預設會選取)，將發生下列情況：  
  
     檔案換用選項會使得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在達到最大檔案大小時，關閉目前的檔案並建立新的檔案。 新檔與前一個檔案同名，但是名稱後會加上一個整數，以指出其順序；例如，如果原始追蹤檔案名為 filename_1.trc，則下一個追蹤檔案名為 filename_2.trc，依此類推。 如果指派給新換用檔案的名稱已為現有檔案所用，除非現有檔案是唯讀，否則會覆寫現有的檔案。 將追蹤資料儲存至檔案時，會預設啟用檔案復原選項。  
  
     檔案換用選項開啟時，追蹤會一直繼續，直到被其他方法停止為止。 若要在您達到檔案大小限制後停止追蹤，請停用檔案換用選項。  
  
    > [!NOTE]  
    >  FAT32 檔案系統的檔案限制為略小於 4 GB。 當追蹤檔案到達該大小時，追蹤即失敗，並產生「磁碟空間不足」錯誤。 若要建立更大的檔案，請使用 NTFS 檔案系統。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
