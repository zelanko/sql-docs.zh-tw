---
title: 選取封裝管理選項 （SSIS 封裝升級精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06cdfdf884dbe4cf63feb441ef5f7665868fc41b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138818"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>選取封裝管理選項 (SSIS 封裝升級精靈)
  使用 [選取封裝管理選項] 頁面，指定用來升級封裝的選項。  
  
 **執行 SSIS 封裝升級精靈**  
  
-   [使用 SSIS 套件升級精靈來升級 Integration Services 套件](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>選項。  
 **更新連接字串以使用新的提供者名稱**  
 更新目前版本之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的連接字串，以使用下列提供者的名稱：  
  
-   OLE DB Provider for [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈] 只會更新儲存在連線管理員中的連接字串。 此精靈不會更新使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 運算式語言或使用指令碼工作中之程式碼以動態方式建構的連接字串。  
  
 **驗證升級套件**  
 驗證升級封裝，並只儲存通過驗證的那些升級封裝。  
  
 如果您不選取這個選項，此精靈將不會驗證升級封裝。 因此，此精靈將會儲存所有的升級封裝，不論封裝是否有效。 此精靈會將升級封裝儲存到精靈之 [選取目的地位置] 頁面上所指定的目的地。  
  
 驗證會增加升級程序的時間。 如果是可能會升級成功的大型封裝，我們建議您不要選取這個選項。  
  
 **建立新的套件識別碼**  
 為升級封裝建立新的封裝識別碼。  
  
 **當套件升級失敗時，繼續升級程序**  
 指定當封裝無法升級時，[ [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈] 應繼續升級其餘的封裝。  
  
 **套件名稱衝突**  
 指定精靈應該要如何處理同名的封裝。 這個選項的值列於下表中。  
  
 **覆寫現有套件檔案**  
 以同名的升級封裝取代現有的封裝。  
  
 **在升級套件名稱後新增數字後置字元**  
 在升級封裝名稱後加入數字後置字元。  
  
 **不升級套件**  
 停止升級封裝，並在完成精靈時顯示錯誤。  
  
 當您在精靈的 [選取目的地位置] 頁面上選取 [儲存至來源位置] 選項時，無法使用這些選項。  
  
 **忽略設定**  
 封裝升級期間不載入封裝組態。 選取此選項可減少升級封裝所需的時間。  
  
 **備份原始套件**  
 讓精靈將原始封裝備份到 **SSISBackupFolder** 資料夾。 此精靈會將 **SSISBackupFolder** 資料夾建立為包含原始封裝和升級封裝之資料夾的子資料夾。  
  
> [!NOTE]  
>  只有當您指定原始封裝和升級封裝儲存在檔案系統和相同的資料夾時，才可使用這個選項。  
  
 如需詳細資訊，請參閱 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
## <a name="see-also"></a>另請參閱  
 [升級 Integration Services 套件](install-windows/upgrade-integration-services-packages.md)  
  
  
