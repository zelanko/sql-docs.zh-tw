---
title: "將資料採礦方案部署到舊版的 SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "回溯相容性 [Analysis Services]"
  - "鑑效組 [資料採礦]"
  - "部署 [Analysis Services]"
  - "時間序列 [Analysis Services]"
  - "部署 [Analysis Services - 資料採礦]"
  - "同步處理 [Analysis Services]"
  - "部署 [Analysis Services]"
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 16
---
# 將資料採礦方案部署到舊版的 SQL Server
  本章節描述當您嘗試將 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 執行個體內建立的資料採礦模型或資料採礦結構部署到使用 SQL Server 2005 Analysis Services 的資料庫，或是當您將 SQL Server 2005 中建立的模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體時，可能發生的相容性問題。  
  
 不支援部署到 SQL Server 2000 Analysis Services 的執行個體。  
  
 [部署時間序列模型](#bkmk_TimeSeries)  
  
 [部署含鑑效組的模型](#bkmk_Holdout)  
  
 [部署含篩選的模型](#bkmk_Filter)  
  
 [從資料庫備份還原](#bkmk_Backup)  
  
 [使用資料庫同步處理](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> 部署時間序列模型  
 Microsoft 時間序列演算法在 SQL Server 2008 中增強了功能，其方式是加入第二個補充性的演算法 ARIMA。 如需時間序列演算法變更的詳細資訊，請參閱 [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)。  
  
 因此，使用新 ARIMA 演算法的時間序列採礦模型的行為可能與部署到 SQL Server 2005 Analysis Services 執行個體時不同。  
  
 如果您已明確設定 PREDICTION_SMOOTHING 參數來控制預測中 ARTXP 和 ARIMA 模型的混用，當您將此模型部署到 SQL Server 2005 執行個體時，Analysis Services 將會引發錯誤，指出此參數無效。 若要避免此錯誤，您必須刪除 PREDICTION_SMOOTHING 參數，並將模型轉換成純正的 ARTXP 模型。  
  
 相反地，如果您要將使用 SQL Server 2005 Analysis Services 建立的時間序列模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體，當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟此採礦模型時，定義檔案會先轉換成新的格式，而且預設會將兩個新的參數加入到所有時間序列模型。 加入的 FORECAST_METHOD 參數具有預設值 MIXED，而且加入的 PREDICTION_SMOOTHING 參數具有預設值 0.5。 但是，此模型將繼續只使用 ARTXP 進行預測，直到重新處理此模型為止。 一旦您重新處理此模型之後，預測就會變更為使用 ARIMA 和 ARTXP 這兩者。  
  
 因此，如果您要避免變更模型，應該只瀏覽模型，而絕對不要處理它。 另外，您也可以明確設定 FORECAST_METHOD 或 PREDICTION_SMOOTHING 參數。  
  
 如需設定混合模型的詳細資訊，請參閱 [Microsoft 時間序列演算法技術參考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
 如果用於模型資料來源的提供者是 SQL Client Data Provider 10，您也必須修改資料來源定義來指定舊版的 SQL Server Native Client。 否則， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 會產生錯誤，指出此提供者尚未註冊。  
  
##  <a name="bkmk_Holdout"></a> 部署含鑑效組的模型  
 如果您使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 來建立包含用於測試資料採礦模型之鑑效組資料分割的採礦結構，此採礦結構可以部署到 SQL Server 2005 執行個體，但是資料分割資訊將會遺失。  
  
 當您在 SQL Server 2005 Analysis Services 中開啟此採礦結構時， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 會引發錯誤，然後重新產生此結構來移除鑑效組資料分割。  
  
 在重新建立此結構之後，[屬性] 視窗中將不再提供鑑效組資料分割的大小；但是，\<ddl100_100:HoldoutMaxPercent>30\</ddl100_100:HoldoutMaxPercent>) 可能仍會存在於 ASSL 指令碼檔案中。  
  
##  <a name="bkmk_Filter"></a> 部署含篩選的模型  
 如果您使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 將篩選套用到採礦模型，此模型可以部署到 SQL Server 2005 執行個體，但是篩選將不會套用。  
  
 當您開啟此採礦模型時， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會引發錯誤，然後重新產生此模型來移除篩選。  
  
##  <a name="bkmk_Backup"></a> 從資料庫備份還原  
 您無法將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立的資料庫備份還原到 SQL Server 2005 執行個體。 如果您這樣做，SQL Server Management Studio 會產生錯誤。  
  
 如果您建立 SQL Server 2005 Analysis Services 資料庫的備份，並將此備份還原到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體，則所有時間序列模型都會修改，如上節所述。  
  
##  <a name="bkmk_Synch"></a> 使用資料庫同步處理  
 不支援從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 到 SQL Server 2005 的資料庫同步處理。  
  
 如果您嘗試同步處理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫，伺服器會傳回錯誤，而且資料庫同步處理會失敗。  
  
## 請參閱＜  
 [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md)  
  
  