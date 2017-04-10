---
title: "使用 SQL Server Agent 在遠端伺服器上設定封裝負載平衡 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "負載平衡 [Integration Services]"
  - "父封裝 [Integration Services]"
  - "SQL Server Agent [Integration Services]"
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 使用 SQL Server Agent 在遠端伺服器上設定封裝負載平衡
  當您必須執行許多封裝時，使用其他可用的伺服器會更方便。 當封裝全都受單一父封裝控制時，使用其他伺服器來執行封裝的這種方法，即稱為負載平衡。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，負載平衡是一種必須由封裝擁有者建構的手動程序。 伺服器並不會自動執行負載平衡。 此外，遠端伺服器上執行的封裝也必須是完整的封裝，而不是其他封裝中的個別工作。  
  
 在下列狀況下，負載平衡非常有用：  
  
-   封裝可以同時執行。  
  
-   封裝規模很大，而且如果連續執行，其執行時間可能超過允許處理的時間。  
  
 管理員和架構設計師可以判斷使用其他伺服器進行處理是否能夠改善其處理效能。  
  
## 負載平衡的圖例說明  
 下圖顯示伺服器上的父封裝。 此父封裝包含多項「執行 SQL 作業代理程式」工作。 父封裝中的每項工作都會呼叫遠端伺服器上的 SQL Server Agent。 這些遠端伺服器包含 SQL Server Agent 作業，而這些作業都有一個步驟可以呼叫該伺服器上的封裝。  
  
 ![SSIS 負載平衡架構概觀](../../integration-services/packages/media/loadbalancingoverview.gif "SSIS 負載平衡架構概觀")  
  
 以這種架構設定負載平衡所需要的步驟並不是新的概念。 相反地，負載平衡是利用現有概念和一般 SSIS 物件，以新的方式來達成。  
  
## 使用 SQL Server Agent 在遠端執行個體執行封裝  
 在遠端封裝執行的基本架構中，中央封裝位於控制其他遠端封裝的 SQL Server 執行個體上。 圖中顯示這個中央封裝，其名稱為 SSIS Parent。 這個父封裝所在的執行個體可控制執行子封裝之 SQL Server Agent 作業的執行。 這些子封裝的執行並未依照遠端伺服器上 SQL Server Agent 所控制的固定排程。 而是在父封裝呼叫時由 SQL Server Agent 啟動這些子封裝，並於 SQL Server Agent 所在的同一個 SQL Server 執行個體上執行。  
  
 您必須先設定父封裝和子封裝，並設定控制子封裝的 SQL Server Agent 作業，才能使用 SQL Server Agent 執行遠端封裝。 下列章節提供有關如何建立、設定、執行及維護遠端伺服器上執行之封裝的詳細資訊。 這個處理程序包含幾個步驟：  
  
-   建立子封裝並將它們安裝在遠端伺服器上。  
  
-   在要執行封裝的遠端執行個體上建立 SQL Server Agent 作業。  
  
-   建立父封裝。  
  
-   決定子封裝的記錄狀況。  
  
 下表提供引導您完成這個處理程序的主題連結。  
  
|主題|說明|  
|-----------|-----------------|  
|[子封裝的實作](../../integration-services/packages/implementation-of-child-packages.md)|描述如何安裝封裝，以及建立 SQL Server Agent 作業來執行封裝。|  
|[父封裝的實作](../../integration-services/packages/implementation-of-the-parent-package.md)|描述如何建立包含許多「執行 SQL Server Agent 作業」工作的父封裝。 每項工作將分別執行其中一個子封裝。|  
|[遠端伺服器上負載平衡封裝的記錄](../../integration-services/packages/logging-for-load-balanced-packages-on-remote-servers.md)|描述遠端封裝的記錄狀況。|  
  
## 相關工作  
 [使用 SQL Server Agent 排程封裝](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
  