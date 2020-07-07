---
title: 建置應用程式
description: 瞭解如何使用 SQL Server Native Client 程式庫來建立應用程式，並從 MDAC、標頭檔和程式庫檔案，以及連接字串進行升級。
ms.custom: ''
ms.date: 12/16/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], building applications
- SQLNCLI, building applications
- applications [SQL Server Native Client]
- SQL Server Native Client, building applications
ms.assetid: 254a2b48-f0e3-43b5-a48d-3d666c2a779f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efb4fea164129627f846571a8a2913afc7097260
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012928"
---
# <a name="building-applications-with-sql-server-native-client"></a>使用 SQL Server Native Client 建立應用程式
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當您開發使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 程式庫的應用程式時，會遇到一些問題。 本章節的主題將討論其中的許多問題，包括從 MDAC 升級到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔和程式庫檔案)，以及可搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用的各種連接字串概觀。  
  
## <a name="in-this-section"></a>本節內容  
 [安裝 SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 討論如何安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client、各種元件的安裝位置，以及如何解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
 [SQL Server Native Client 的元件](../../../relational-databases/native-client/applications/components-of-sql-server-native-client.md)  
 討論組成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的元件，包括程式庫、資源、說明和標頭檔案。  
  
 [搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
 討論當透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 連接到資料庫時，可以使用之各種類型的連接字串。  
  
 [使用 SQL Server Native Client 標頭檔與程式庫檔案](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)  
 討論如何在應用程式內使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔和程式庫檔案。  
  
 [從 MDAC 將應用程式更新至 SQL Server Native Client](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 與 MDAC 之間的差異以及從 MDAC 升級到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時所應該考量的問題。  
  
 [從 SQL Server 2005 Native Client 更新應用程式](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)  
 討論從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 升級到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 時所應該考量的問題。  
  
 [使用 ADO 搭配 SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)  
 討論 ADO 要如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 來存取及使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能。  
  
 [SQL Server Native Client 的支援原則](../../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md)  
 討論要如何搭配不同版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用各種資料存取元件。  
  
 [使用 SQL Server Native Client 連線到 Azure SQL Database](../../../relational-databases/native-client/applications/connecting-to-a-windows-azure-sql-database-using-sql-server-native-client.md)  
 討論如何使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client 連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 的使用說明主題](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 的使用說明主題](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
