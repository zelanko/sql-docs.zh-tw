---
title: "網路屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "LingerTimeout 屬性"
  - "EnableNagleAlgorithm 屬性"
  - "MinPendingAcceptExCount 屬性"
  - "MaxPendingSendCount 屬性"
  - "EnableBinaryXML 屬性"
  - "MinPendingReceiveCount 屬性"
  - "MaxCompletedReceiveCount屬性"
  - "DisableNonblockingMode 屬性"
  - "RequestSizeThreshold 屬性"
  - "CompressionLevel 屬性"
  - "ReceiveBufferSize 屬性"
  - "EnableCompression 屬性"
  - "ServerSendTimeout 屬性"
  - "IPV4Support 屬性"
  - "MaxPendingReceiveCount 屬性"
  - "MaxPendingAcceptExCount 屬性"
  - "IPV6Support 屬性"
  - "MaxAllowedRequestSize 屬性"
  - "ServerReceiveTimeout 屬性"
  - "EnableLingerOnClose 屬性"
  - "InitialConnectTimeout 屬性"
  - "SendBufferSize 屬性"
  - "ScatterReceiveMultiplier 屬性"
  - "網路屬性 [Analysis Services]"
ms.assetid: ef4251e2-abe5-4c5b-9868-7549782d0244
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# 網路屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## 一般  
 **ListenOnlyOnLocalConnections**  
 此為布林值屬性，識別是否僅在本機連接上接聽，例如 localhost。  
  
## 接聽程式  
 **IPV4Support**  
 此為帶正負號的 32 位元整數屬性，定義 IPv4 通訊協定的支援。 此屬性的值為下表列出的值之一：  
  
|Value|描述|  
|-----------|-----------------|  
|*0*|IPv4 已停用；用戶端無法連接。|  
|*1*|(預設值) 需要有 IPv4；如果伺服器無法接聽 IPv4 將無法啟動。|  
|*2*|IPv4 是選擇性的；伺服器會嘗試接聽 IPv4，但即使無法接聽仍會啟動。|  
  
 **IPV6Support**  
 此為帶正負號的 32 位元整數屬性，定義 IPv6 通訊協定的支援。 此屬性的值為下表列出的值之一：  
  
|Value|描述|  
|-----------|-----------------|  
|*0*|IPv6 已停用；用戶端無法連接。|  
|*1*|(預設值) 需要有 IPv6；如果伺服器無法接聽 IPv6 將無法啟動。|  
|*2*|IPv6 是選擇性的；伺服器會嘗試接聽 IPv6，但即使無法接聽仍會啟動。|  
  
 **MaxAllowedRequestSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **RequestSizeThreshold**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **ServerReceiveTimeout**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **ServerSendTimeout**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## 要求  
 **EnableBinaryXML**  
 此為布林值屬性，指定伺服器是否會辨識要求的二進位 XML 格式。  
  
 **EnableCompression**  
 此為布林值屬性，指定是否針對要求啟用壓縮。  
  
## 回應  
 **CompressionLevel**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **EnableBinaryXML**  
 此為布林值屬性，指定伺服器是否啟用二進位 XML 回應。  
  
 **EnableCompression**  
 此為布林值屬性，指定是否針對用戶端要求的回應啟用壓縮。  
  
## TCP  
 **InitialConnectTimeout**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MaxCompletedReceiveCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MaxPendingAcceptExCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MaxPendingReceiveCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MaxPendingSendCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MinPendingAcceptExCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MinPendingReceiveCount**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **ScatterReceiveMultiplier**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\ DisableNonblockingMode**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\ EnableLingerOnClose**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\EnableNagleAlgorithm**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\ LingerTimeout**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\ ReceiveBufferSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SocketOptions\ SendBufferSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## 請參閱＜  
 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  