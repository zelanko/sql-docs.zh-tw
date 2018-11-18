---
title: 從命令提示字元安裝更新 | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: c69d17094d5998c0158aeb56d8c14421f6199a4b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605985"
---
# <a name="installing-updates-from-the-command-prompt"></a>從命令提示字元安裝更新

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

測試並修改安裝指令碼，以便符合組織的需求。 
 
## <a name="sample-syntax-for-installation"></a>安裝的範例語法 
更新封裝的名稱會有所不同而且可能包含語言、版本及處理器元件。 在命令提示字元中套用更新，並以您的更新封裝名稱取代 <package_name>： 
 
- 更新單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體及所有共用元件，類似 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具：您可以使用 InstanceName 參數或 InstanceID 參數來指定執行個體。 若要更新備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，您必須指定 InstanceID 參數。

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance
    ```
    中的多個 
    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>. 
    ```

- 安裝程式可以整合最新產品更新與主要產品安裝，因此主要產品及其適用的更新可以同時安裝。 您可以準備資料庫引擎執行個體安裝，以包含產品更新： 

    ```
    setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateSource=\<path where the update is downloaded> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine. 
    ```

- 僅更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用元件，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具： 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch 
    ```

- 更新電腦上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和所有共用元件，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具： 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances. 
    ```

- 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 單一執行個體和所有共用元件中移除更新，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具： 

    ```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance. 
    ```

- 僅移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用元件的更新，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具： 

    ```
    <package_name>.exe /qs /Action=RemovePatch 
    ```

  > [!NOTE] 
  > 更新安裝程式會確保共用元件一定處於執行個體版本的最高層級或最高層級以上。 
 
## <a name="supported-parameters"></a>支援的參數 
 
> [!IMPORTANT] 
> 可能的話，請在執行階段提供安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。 
 
|參數|Description| 
|------------|-----------------| 
|**/?**|顯示自動安裝命令提示字元說明。| 
|**/action=Patch 或 /action=RemovePatch**|指定安裝動作：Patch 或 RemovePatch。| 
|**/allinstances**|將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新套用至所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用的非執行個體感知元件。| 
|**/instancename=InstanceName***|將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新套用至名為 InstanceName 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用的非執行個體感知元件。| 
|**/InstanceID=Inst1**|將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 執行個體以及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用的非執行個體感知元件。| 
|**/quiet**|以自動安裝模式執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新安裝程式。| 
|**/qs**|只顯示進度 UI 對話方塊。| 
|**/UpdateEnabled**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式是否應該探索及包含產品更新。 有效值為 True 和 False 或 1 和 0。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會包含找到的更新。| 
|**/IAcceptSQLServerLicenseTerms**|只有當您針對自動安裝指定了 /Q 或 /QS 參數時，才需要使用此參數。| 
 
 *您不能指定這個參數來將更新套用到備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 您必須改為指定 /instanceID 參數。 
 
## <a name="see-also"></a>另請參閱 
 [SQL Server 服務安裝概觀](https://msdn.microsoft.com/library/6a9fd19b-2367-4908-b638-363b1e929e1e) 
 
 
