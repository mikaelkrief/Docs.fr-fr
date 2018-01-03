---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: "Utilisez ViewData et implémentez ViewModel Classes | Documents Microsoft"
author: microsoft
description: "Étape 6 montre comment activer la prise en charge de la modification de scénarios, de forme plus riche et présente également les deux approches qui peuvent être utilisés pour passer des données à partir des contrôleurs à des vues :..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 36b9e87cc24f74f7f2cc592afb5102709b598f74
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="95c3b-103">Utilisez ViewData et implémenter les Classes ViewModel</span><span class="sxs-lookup"><span data-stu-id="95c3b-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="95c3b-104">par [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="95c3b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="95c3b-105">Télécharger le PDF</span><span class="sxs-lookup"><span data-stu-id="95c3b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="95c3b-106">Il s’agit d’étape 6 a gratuit [« « l’application NerdDinner](introducing-the-nerddinner-tutorial.md) qui parcours à comment générer un petit, mais se termine, application web à l’aide d’ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="95c3b-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="95c3b-107">Étape 6 montre comment activer la prise en charge de la modification de scénarios, de forme plus riche et présente également les deux approches qui peuvent être utilisés pour passer des données à partir des contrôleurs à des vues : ViewData et ViewModel.</span><span class="sxs-lookup"><span data-stu-id="95c3b-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="95c3b-108">Si vous utilisez ASP.NET MVC 3, nous vous recommandons de suivre les [mise en route a démarré avec MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [magasin de musique MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) didacticiels.</span><span class="sxs-lookup"><span data-stu-id="95c3b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="95c3b-109">NerdDinner étape 6 : ViewData et ViewModel</span><span class="sxs-lookup"><span data-stu-id="95c3b-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="95c3b-110">Nous avons couvert un nombre de scénarios de publication de formulaire et décrit comment implémenter créer, mettre à jour et supprimer la prise en charge (CRUD).</span><span class="sxs-lookup"><span data-stu-id="95c3b-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="95c3b-111">Maintenant nous prendre notre implémentation DinnersController complémentaires et activer la prise en charge de la modification de scénarios de formulaire plus riche.</span><span class="sxs-lookup"><span data-stu-id="95c3b-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="95c3b-112">Lors de cette opération, nous verrons deux approches qui peuvent être utilisés pour passer des données à partir des contrôleurs à des vues : ViewData et ViewModel.</span><span class="sxs-lookup"><span data-stu-id="95c3b-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="95c3b-113">Passage de données à partir des contrôleurs pour afficher les modèles</span><span class="sxs-lookup"><span data-stu-id="95c3b-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="95c3b-114">Une des caractéristiques de définition du modèle MVC est stricte « séparation des responsabilités » il permet d’appliquer entre les différents composants d’une application.</span><span class="sxs-lookup"><span data-stu-id="95c3b-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="95c3b-115">Les modèles, les contrôleurs et les vues chacun ont bien définie de rôles et responsabilités, et ils communiquent entre eux de façons bien définies.</span><span class="sxs-lookup"><span data-stu-id="95c3b-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="95c3b-116">Cela permet de promouvoir la testabilité et réutilisation du code.</span><span class="sxs-lookup"><span data-stu-id="95c3b-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="95c3b-117">Quand une classe de contrôleur décide de restituer une réponse HTML à un client, il est responsable en fournissant explicitement pour le modèle d’affichage de toutes les données nécessaires au rendu de la réponse.</span><span class="sxs-lookup"><span data-stu-id="95c3b-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="95c3b-118">Afficher les modèles ne doivent jamais exécuter toute logique d’application ou de récupération de données – et doivent se pour disposer uniquement le code de rendu qui est basée sur les modèle/des données transmises par le contrôleur de limiter à la place.</span><span class="sxs-lookup"><span data-stu-id="95c3b-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="95c3b-119">Maintenant les données du modèle passé par notre DinnersController classe nos modèles de vue est simple et directe : une liste d’objets dîner dans le cas Index() et un dîner unique de l’objet dans le cas Details(), Edit(), Create() et Delete().</span><span class="sxs-lookup"><span data-stu-id="95c3b-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="95c3b-120">Comme nous ajouter davantage de capacités de l’interface utilisateur à notre application, nous allons souvent ont besoin de transmettre plus que ces données pour effectuer le rendu des réponses HTML dans nos modèles de vue.</span><span class="sxs-lookup"><span data-stu-id="95c3b-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="95c3b-121">Par exemple, nous souhaitons pouvons modifier le champ « Pays » au sein de notre modifier et créer des vues d’en cours d’une zone de texte HTML à une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="95c3b-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="95c3b-122">Au lieu de coder en dur la liste déroulante des noms de pays dans le modèle d’affichage, nous pouvons si vous le souhaitez générer à partir d’une liste de pays pris en charge qui nous remplir dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="95c3b-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="95c3b-123">Nous devons permettent de passer à la fois l’objet Dinner *et* la liste des pays pris en charge à partir de notre contrôleur à nos modèles de vue.</span><span class="sxs-lookup"><span data-stu-id="95c3b-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="95c3b-124">Nous allons étudier deux façons, que nous pouvons effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="95c3b-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="95c3b-125">À l’aide du dictionnaire ViewData</span><span class="sxs-lookup"><span data-stu-id="95c3b-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="95c3b-126">La classe de base du contrôleur expose une propriété au dictionnaire « ViewData » qui peut être utilisée pour passer des éléments de données à partir des contrôleurs à des vues.</span><span class="sxs-lookup"><span data-stu-id="95c3b-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="95c3b-127">Par exemple, pour prendre en charge le scénario où nous voulons modifier la zone de texte « Pays » dans la vue d’édition ne soient pas d’une zone de texte HTML à une liste déroulante, nous pouvons mettre à jour notre méthode d’action Edit() pour transmettre (en plus d’un objet Dinner) un objet SelectList qui peut être utilisé comme mesure odèle de dropdownlist pays.</span><span class="sxs-lookup"><span data-stu-id="95c3b-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="95c3b-128">Le constructeur de la SelectList ci-dessus accepte une liste de comtés pour remplir la liste-downlist avec, ainsi que la valeur actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="95c3b-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="95c3b-129">Nous pouvons ensuite mettre à jour notre modèle de vue Edit.aspx pour utiliser la méthode d’assistance Html.DropDownList() au lieu de la méthode d’assistance Html.TextBox() que nous avons utilisé précédemment :</span><span class="sxs-lookup"><span data-stu-id="95c3b-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="95c3b-130">La méthode d’assistance Html.DropDownList() ci-dessus accepte deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="95c3b-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="95c3b-131">Le premier est le nom de l’élément de formulaire HTML en sortie.</span><span class="sxs-lookup"><span data-stu-id="95c3b-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="95c3b-132">Le deuxième est le modèle « SelectList » nous avons transmis via le dictionnaire ViewData.</span><span class="sxs-lookup"><span data-stu-id="95c3b-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="95c3b-133">Nous utilisons c# mot clé « as » pour effectuer un cast de type au sein du dictionnaire en tant qu’un SelectList.</span><span class="sxs-lookup"><span data-stu-id="95c3b-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="95c3b-134">Et maintenant quand nous exécutons notre accès aux applications et le */Dinners/Edit/1* URL dans votre navigateur, nous allons voir que notre interface utilisateur de modification a été mis à jour pour afficher une liste déroulante des pays au lieu d’une zone de texte :</span><span class="sxs-lookup"><span data-stu-id="95c3b-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="95c3b-135">Étant donné que nous avons rendu également le modèle de vue de modification de la méthode HTTP-POST modifier (dans les scénarios de cas d’erreur), nous vous souhaitez vous assurer que nous avons également mettre à jour cette méthode pour ajouter le SelectList à ViewData lorsque le modèle d’affichage est rendu dans les scénarios d’erreur :</span><span class="sxs-lookup"><span data-stu-id="95c3b-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="95c3b-136">Et maintenant notre scénario de modification DinnersController prend en charge une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="95c3b-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="95c3b-137">Utilisation d’un modèle ViewModel</span><span class="sxs-lookup"><span data-stu-id="95c3b-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="95c3b-138">L’approche de dictionnaire ViewData présente l’avantage d’être relativement rapide et facile à implémenter.</span><span class="sxs-lookup"><span data-stu-id="95c3b-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="95c3b-139">Certains développeurs n’aiment pas à l’aide de dictionnaires basés sur chaîne, cependant, étant donné que les fautes de frappe peuvent entraîner des erreurs qui ne sont pas interceptées au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="95c3b-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="95c3b-140">Le dictionnaire ViewData non typé requiert également à l’aide de l’opérateur « as » ou de conversion lors de l’utilisation d’un langage fortement typé tel que c# dans un modèle d’affichage.</span><span class="sxs-lookup"><span data-stu-id="95c3b-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="95c3b-141">Une autre approche que nous pourrions utiliser est un est souvent appelé le motif « View ».</span><span class="sxs-lookup"><span data-stu-id="95c3b-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="95c3b-142">Lors de l’utilisation de ce modèle, nous créons des classes fortement typées qui sont optimisés pour nos scénarios d’affichage spécifiques, et qui expose les propriétés pour le valeurs/contenu dynamique nécessaire par nos modèles de vue.</span><span class="sxs-lookup"><span data-stu-id="95c3b-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="95c3b-143">Nos classes de contrôleur peuvent remplir, puis passer ces classes optimisées en vue de notre modèle d’affichage à utiliser.</span><span class="sxs-lookup"><span data-stu-id="95c3b-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="95c3b-144">Cela permet la sécurité de type, la vérification de la compilation et intellisense de l’éditeur dans les modèles d’affichage.</span><span class="sxs-lookup"><span data-stu-id="95c3b-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="95c3b-145">Par exemple, pour activer le formulaire dinner éditions scénarios que nous pouvons créer un « DinnerFormViewModel » classe comme ci-dessous qui expose deux propriétés fortement typées : un objet dîner et le modèle SelectList requis pour remplir le dropdownlist pays :</span><span class="sxs-lookup"><span data-stu-id="95c3b-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="95c3b-146">Nous pouvons ensuite mettre à jour notre méthode d’action Edit() pour créer le DinnerFormViewModel à l’aide de l’objet Dinner que nous récupérons à partir de notre référentiel et passez-lui à notre modèle de vue :</span><span class="sxs-lookup"><span data-stu-id="95c3b-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="95c3b-147">Nous allons ensuite la mise à jour notre modèle d’affichage afin qu’elle attend un « DinnerFormViewModel » au lieu d’un « dîner » de l’objet en modifiant l’attribut « inherits » en haut de la page edit.aspx comme suit :</span><span class="sxs-lookup"><span data-stu-id="95c3b-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="95c3b-148">Une fois que cela, nous, intellisense de la propriété « Modèle » au sein de notre modèle de vue sera mis à jour pour refléter le modèle d’objet du type DinnerFormViewModel que nous sommes en lui passant :</span><span class="sxs-lookup"><span data-stu-id="95c3b-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="95c3b-149">Nous pouvons ensuite mettre à jour notre code afficher travailler dessus.</span><span class="sxs-lookup"><span data-stu-id="95c3b-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="95c3b-150">Remarquez ci-dessous comment nous modifions pas les noms des éléments d’entrée, nous allons créer (les éléments de formulaire seront toujours nommés « Title », « Pays »), mais nous allons mettre à jour les méthodes de programme d’assistance HTML pour extraire les valeurs à l’aide de la classe DinnerFormViewModel :</span><span class="sxs-lookup"><span data-stu-id="95c3b-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="95c3b-151">Nous allons également mettre à jour notre méthode post de modifier pour utiliser la classe DinnerFormViewModel lors du rendu des erreurs :</span><span class="sxs-lookup"><span data-stu-id="95c3b-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="95c3b-152">Nous pouvons également mettre à jour nos méthodes d’action Create() réutiliser le même *DinnerFormViewModel* classe pour permettre les pays DropDownList dans celles ainsi.</span><span class="sxs-lookup"><span data-stu-id="95c3b-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="95c3b-153">Voici l’implémentation HTTP-GET :</span><span class="sxs-lookup"><span data-stu-id="95c3b-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="95c3b-154">Voici l’implémentation de la méthode HTTP-POST créer :</span><span class="sxs-lookup"><span data-stu-id="95c3b-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="95c3b-155">En maintenant nos écrans modifier et créer des listes déroulantes pour la sélection du pays.</span><span class="sxs-lookup"><span data-stu-id="95c3b-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="95c3b-156">Classes de ViewModel en forme personnalisée</span><span class="sxs-lookup"><span data-stu-id="95c3b-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="95c3b-157">Dans le scénario ci-dessus, notre classe DinnerFormViewModel expose directement l’objet de modèle Dinner en tant que propriété, ainsi que d’une propriété de modèle SelectList prise en charge.</span><span class="sxs-lookup"><span data-stu-id="95c3b-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="95c3b-158">Cette approche fonctionne pour les scénarios où l’interface utilisateur HTML que nous voulons créer au sein de notre modèle d’affichage correspond relativement à nos objets de modèle de domaine.</span><span class="sxs-lookup"><span data-stu-id="95c3b-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="95c3b-159">Pour les scénarios où cela n’est pas le cas, une option que vous pouvez utiliser consiste à créer une classe de ViewModel en forme personnalisée dont le modèle objet est plus optimisé pour la consommation par la vue, et qui peut se présenter complètement différent de l’objet de modèle de domaine sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="95c3b-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="95c3b-160">Par exemple, elle peut potentiellement exposer les noms des propriétés et/ou des propriétés d’agrégation recueillies à partir de plusieurs objets de modèle.</span><span class="sxs-lookup"><span data-stu-id="95c3b-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="95c3b-161">Les classes ViewModel en forme personnalisées peuvent être utilisées à la fois pour passer des données à partir des contrôleurs à des vues à restituer, ainsi que pour aider à gérer les données de formulaire publiées sur la méthode d’action d’un contrôleur.</span><span class="sxs-lookup"><span data-stu-id="95c3b-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="95c3b-162">Pour ce scénario plus loin, vous disposez peut-être la méthode d’action mettre à jour un objet ViewModel avec les données de formulaire publié, puis utiliser l’instance ViewModel mapper ou récupérer un objet de modèle de domaine réel.</span><span class="sxs-lookup"><span data-stu-id="95c3b-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="95c3b-163">Classes de ViewModel en forme personnalisée peuvent fournir une grande souplesse et sont quelque chose à examiner chaque fois que vous recherchez le code de rendu dans vos modèles d’affichage ou le code de validation de formulaire à l’intérieur de vos méthodes d’action commence à se compliquer trop.</span><span class="sxs-lookup"><span data-stu-id="95c3b-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="95c3b-164">Il s’agit souvent un signe que vos modèles de domaine correctement ne correspondent pas à l’interface utilisateur que vous générez, et qu’une classe de ViewModel intermédiaire en forme personnalisée peut aider.</span><span class="sxs-lookup"><span data-stu-id="95c3b-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="95c3b-165">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="95c3b-165">Next Step</span></span>

<span data-ttu-id="95c3b-166">Nous allons maintenant voir comment nous pouvons utiliser aucun et les pages maîtres pour réutiliser et partager l’interface utilisateur dans notre application.</span><span class="sxs-lookup"><span data-stu-id="95c3b-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="95c3b-167">[Précédent](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Suivant](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="95c3b-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>