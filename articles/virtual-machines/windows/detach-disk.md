---
title: Détacher un disque de données d’une machine virtuelle Windows – Azure
description: Détachez un disque de données d’une machine virtuelle dans Azure à l’aide du modèle de déploiement Resource Manager.
author: cynthn
ms.service: virtual-machines-windows
ms.subservice: disks
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 01/26/2021
ms.author: cynthn
ms.openlocfilehash: a995cd1d02438ae3be7091ba55e945549558829d
ms.sourcegitcommit: d1e56036f3ecb79bfbdb2d6a84e6932ee6a0830e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2021
ms.locfileid: "99055193"
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a>Détachement d’un disque de données d’une machine virtuelle Windows

Lorsque vous n’avez plus besoin d’un disque de données qui est attaché à une machine virtuelle, vous pouvez le détacher facilement. Cela supprime le disque de la machine virtuelle, mais pas du stockage.

> [!WARNING]
> Si vous détachez un disque, il n’est pas supprimé automatiquement. Si vous êtes abonné au stockage Premium, vous continuerez à engager des frais de stockage pour le disque. Pour plus d’informations, consultez [Tarifs et facturation du stockage Premium](../disks-types.md#billing).

Si vous souhaitez réutiliser les données du disque, vous pouvez l’attacher à la même machine virtuelle ou à une autre.

 

## <a name="detach-a-data-disk-using-powershell"></a>Détacher un disque de données avec PowerShell

Vous pouvez supprimer *à chaud* un disque de données à l’aide de PowerShell, mais vérifiez qu’il n’est pas activement utilisé avant de le détacher de la machine virtuelle.

Dans cet exemple, nous supprimons le disque nommé **myDisk** de la machine virtuelle **myVM** dans le groupe de ressources **myResourceGroup**. Vous commencez par supprimer le disque à l'aide de la cmdlet [Remove-AzVMDataDisk](/powershell/module/az.compute/remove-azvmdatadisk). Puis vous mettez à jour l'état de la machine virtuelle à l'aide de la cmdlet [Update-AzVM](/powershell/module/az.compute/update-azvm) pour finaliser le processus de suppression du disque de données.

```azurepowershell-interactive
$VirtualMachine = Get-AzVM `
   -ResourceGroupName "myResourceGroup" `
   -Name "myVM"
Remove-AzVMDataDisk `
   -VM $VirtualMachine `
   -Name "myDisk"
Update-AzVM `
   -ResourceGroupName "myResourceGroup" `
   -VM $VirtualMachine
```

Le disque reste dans le stockage, mais il n’est plus attaché à une machine virtuelle.

## <a name="detach-a-data-disk-using-the-portal"></a>Détacher un disque de données avec le portail

Vous pouvez supprimer *à chaud* un disque de données, mais vérifiez cependant qu’il n’est pas activement utilisé avant de le détacher de la machine virtuelle.

1. Dans le menu de gauche, sélectionnez **Machines virtuelles**.
1. Sélectionnez la machine virtuelle qui a le disque de données que vous voulez détacher.
1. Sous **Paramètres**, sélectionnez **Disques**.
1. Dans le volet **Disques**, tout à droite du disque de données que vous voulez détacher, cliquez sur le bouton de détachement **X**.
1. Sélectionnez **Enregistrer** en haut de la page pour enregistrer vos modifications.

Le disque reste dans le stockage, mais il n’est plus attaché à une machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez réutiliser le disque de données, vous pouvez simplement l’[attacher à une autre machine virtuelle](attach-managed-disk-portal.md).

Si vous souhaitez supprimer le disque afin d’éviter les coûts de stockage, consultez [Recherche et suppression des disques Azure non attachés (managés ou non) – Portail Azure](../disks-find-unattached-portal.md).
