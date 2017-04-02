---
title: "報表伺服器應用程式的應用程式網域 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "應用程式網域 [Reporting Services]"
  - "回收應用程式網域"
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# 報表伺服器應用程式的應用程式網域
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，報表伺服器會實作成單一服務，其中包含報表伺服器 Web 服務、報表管理員和背景處理應用程式。 每個應用程式都會在單一報表伺服器處理序內部的應用程式網域中執行。 在大部分情況下，應用程式網域是在內部建立、設定和管理的。 不過，如果您要調查效能或記憶體問題或者疑難排解服務中斷，了解報表伺服器應用程式網域的回收作業如何發生可能會很有用。  
  
> [!NOTE]  
>  如果您在使用基本驗證的報表伺服器上設定報表產生器存取，報表產生器將會在它自己的應用程式網域內執行。 此應用程式網域與在伺服器處理序內執行的其他應用程式網域不同。 它是由服務控制程式所管理，而且不受記憶體管理功能的約束 (該項功能會重新調整記憶體配置，以回應報表伺服器上記憶體不足的壓力)。  
  
 下列清單將描述導致 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式之應用程式網域回收作業發生的事件：  
  
-   以預先定義間隔發生的排程回收作業。  
  
-   報表伺服器的組態變更。  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 組態變更。  
  
-   記憶體配置失敗。  
  
 下表將摘要列出為了回應這些事件所發生的應用程式網域回收行為：  
  
|事件|事件描述|適用於|可設定|回收作業描述|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|以預先定義間隔發生的排程回收作業|根據預設，應用程式網域每隔 12 小時會回收一次。<br /><br /> 排程回收作業是提升整體處理序健全狀況之 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式的常見作法。|報表伺服器 Web 服務<br /><br /> 報表管理員<br /><br /> 背景處理應用程式|是的。 RSReportServer.config 檔中的**RecycleTime** 組態設定會決定回收間隔。<br /><br /> **MaxAppDomainUnloadTime** 會設定允許背景處理完成的等候時間。|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 會管理 Web 服務和報表管理員的回收作業。<br /><br /> 若為背景處理應用程式，報表伺服器會針對從排程起始的新作業建立新的應用程式網域。 系統會允許已經在進行中的作業在目前的應用程式網域中完成，直到等候時間過期為止。|  
|報表伺服器的組態變更|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 將回收應用程式網域，以便回應 RSReportServer.config 檔中的變更。|報表伺服器 Web 服務<br /><br /> 報表管理員<br /><br /> 背景處理應用程式|資料分割|您無法阻止回收作業發生。 不過，為了回應組態變更所發生之回收作業的處理方式與排程回收作業相同。 當目前的要求和作業在目前的應用程式網域中完成時，系統會針對新的要求建立新的應用程式網域。|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 組態變更|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 如果所監視的檔案 (例如，machine.config 和 Web.config 檔，以及 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 程式檔案) 發生變更，它就會回收應用程式網域。|報表伺服器 Web 服務<br /><br /> 報表管理員|資料分割|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 會管理此作業。<br /><br /> 由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 起始的回收作業不會影響背景處理應用程式網域。|  
|記憶體不足的壓力和記憶體配置失敗|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR 就會立即回收應用程式網域。|報表伺服器 Web 服務<br /><br /> 報表管理員<br /><br /> 背景處理應用程式|資料分割|處於高度記憶體不足壓力的情況下，報表伺服器不會接受目前應用程式網域中的新要求。 在伺服器拒絕新要求的期間，就會發生 HTTP 503 錯誤。 卸載舊的應用程式網域之前，系統不會建立新的應用程式網域。 這表示，如果您在伺服器處於高度記憶體不足壓力的情況下進行組態檔變更，正在進行中的要求和作業可能無法啟動或完成。<br /><br /> 如果記憶體配置失敗，所有應用程式網域都會立即重新啟動。 系統會卸除正在進行中的作業和要求。 您必須以手動方式重新啟動這些作業和要求。|  
  
## 已規劃與未規劃的回收作業  
 回收作業是已規劃或未規劃完全取決於產生作業的條件而定：  
  
-   已規劃的回收作業會以 RSReportServer.config 檔中定義的固定間隔發生。 預設值為每隔 12 小時。 這是提升整體處理序健全狀況之 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式的常見作法。 若為已規劃的回收作業，報表伺服器會針對新的要求建立其他應用程式網域。 系統會允許已經在進行中的要求在目前的應用程式網域中完成，直到等候時間過期為止。 管理已規劃回收作業的組態設定是針對整個伺服器設定的。 您無法針對每個應用程式設定不同的回收排程或記憶體臨界值。  
  
-   未規劃的回收作業會在任意時間發生，以便回應組態變更、記憶體不足的壓力，以及記憶體配置失敗：  
  
    -   若為組態變更，報表伺服器將嘗試使用軟式回收，以便將新的要求重新導向至應用程式網域的新執行個體。 如果軟式回收失敗，伺服器就會起始硬式應用程式網域回收，以便取消所有進行中的要求、關閉目前的應用程式網域，然後重新啟動應用程式網域。  
  
    -   記憶體配置失敗是表示系統資源不足，無法提供伺服器所執行之報表處理的資源量。 為了回應記憶體配置失敗，系統會針對所有應用程式網域進行硬式回收作業。 所有要求佇列都會清除。 已取消的要求不會重新啟動。 以互動方式檢視報表的使用者必須重新整理或重新開啟報表。 排程的處理將在下一個排程的時間發生。 如果無法接受延遲，您可以手動重新整理報表快照集，或修改訂閱排程或報表快照集排程，讓它立即執行。  
  
 報表伺服器 Web 服務、報表管理員和背景處理應用程式的應用程式網域可能會一起回收或個別回收，端視導致回收發生的情況而定：  
  
-   由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 起始的回收作業通常只會影響 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式：報表伺服器 Web 服務和報表管理員。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 所監視的檔案發生變更，它就會回收應用程式網域。 由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 起始的回收作業通常與背景處理應用程式的回收作業無關。  
  
-   由報表伺服器起始的回收作業通常會影響報表伺服器 Web 服務、報表管理員和背景處理應用程式。 為了回應組態設定和服務重新啟動的變更，系統會進行回收作業。  
  
## 應用程式網域的 RSReportServer 組態設定  
 組態設定指定於 [RSReportServer.config 檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)中。 下列範例會顯示已規劃應用程式網域回收行為的預設組態設定。  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 下表將描述這些元素。  
  
|元素|適用對象|定義|  
|-------------|----------------|----------------|  
|**RecycleTime**|這三個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式網域|指定回收應用程式網域的頻率。 預設回收排程符合通常在 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式網域回收中所遵循的 12 小時制模式。 在排程的時間，所有新要求都會轉送至應用程式網域的新執行個體。 目前正在原始執行個體進行中的要求可以繼續執行到完成。 等到所有處理序都完成後，系統會刪除原始執行個體，而新執行個體將成為唯一使用中的應用程式網域執行個體。<br /><br /> 預設值為 720 分鐘。|  
|**MaxAppDomainUnloadTime**|只有背景處理應用程式網域|根據預設，報表伺服器會配置 30 分鐘的等候時間，在這段時間內，允許在回收作業過程中關閉應用程式網域。 如果目前進行中的作業無法在指定的時間內完成 (或者作業所花的時間比等候時間所允許的還要久)，系統就會立即重新啟動應用程式網域執行個體。 所有未完成的作業都會結束。<br /><br /> 如需如何檢視或取消在報表伺服器上執行之作業的詳細資訊，請參閱[取消報表伺服器作業 &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)。|  
  
> [!NOTE]  
>  雖然報表伺服器 Web 服務和報表管理員是 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式，但是這兩個應用程式都不會回應排程應用程式網域回收 (可能已在 IIS 中主控之 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式的 machine.config 中指定)。  
  
## 請參閱＜  
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  