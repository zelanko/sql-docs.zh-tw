---
title: 偵錯工具預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90b72b0e60550b0b6bdf89e0ba39e6089c5d8de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727744"
---
# <a name="debugging-stored-procedures"></a>除錯預存程序
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預存程序實際上是以 C# (或任何其他 CLR 或 COM 語言) 撰寫的 CLR 或 COM 程式庫 (通常是 DLL)。 因此，偵錯預存程序十分類似在 Visual Studio 偵錯環境中除錯任何其他應用程式。 您可以使用整合偵錯功能，在 Visual Studio 開發環境中偵錯預存程序。 它們可讓您在程序位置上停止，檢查記憶體和登錄值，變更變數，觀察訊息流量，以及仔細查看程式碼的運作方式。  
  
### <a name="to-debug-a-stored-procedure"></a>偵錯預存程序  
  
1.  開啟用於 Visual Studio 中建立 DLL 的專案。  
  
2.  在對應到您要偵錯之程序的方法或函數中建立中斷點。  
  
3.  使用 Visual Studio 建立預存程序 DLL 的偵錯建置。  
  
4.  將 DLL 部署到伺服器。 如需將 DLL 部署至伺服器的詳細資訊，請參閱[建立預存程式](creating-stored-procedures.md)。  
  
5.  您需要一個應用程式來呼叫您要測試的預存程序。 如果您還沒有這樣的應用程式，可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 MDX 查詢編輯器，建立一個 MDX 查詢來呼叫您要測試的預存程序。  
  
6.  在 Visual Studio 中，附加至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理序 (Msmdsrv.exe)。  
  
    1.  從 [**調試**] 功能表中，選擇 [**附加 toProcess**]。  
  
    2.  在 [**附加 toProcess** ] 對話方塊中，選取 [**顯示所有使用者的進程**]。  
  
    3.  在 [**可使用的進程**] 清單中，按一下 [**處理**] 資料行中的 [ **msmdsrv.exe**]。 如果在伺服器上執行一個以上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，您需要以您要使用之執行個體的識別碼來識別處理序。  
  
    4.  在 [**附加至**] 文字方塊中，確認已選取適當的程式類型。 若為 CLR DLL，請依序按一下 [**選取**]、[**偵錯工具代碼類型**] 和 [**受管理**]，然後按一下 **[確定]**。 若為 COM DLL，請依序按一下 [**選取**]、[**偵錯工具代碼類型**] 和 [**原生**]，然後按一下 **[確定]**。  
  
    5.  按一下 [附加] ****。  
  
7.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，叫用程式或 MDX 指令碼來呼叫預存程序。 當偵錯工具到達包含中斷點的那一行時就會中斷。 您可以在監看式視窗中評估變數、檢視地區設定和逐步執行程式碼。  
  
 如果您在偵錯程式庫時發生問題，請確定對應的程式資料庫 (PDB) 檔案已複製到伺服器上的部署位置。 如果在註冊或部署期間未複製此檔案，您必須手動將它複製到與 DLL 相同的位置。 若為機器碼 (COM DLL)，PDB 檔是位於 \debug 子目錄中。 若為 Managed 程式碼 (CLR DLL)，它位於 \WINDEBUG 子目錄中。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型元件管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](defining-stored-procedures.md)  
  
  
