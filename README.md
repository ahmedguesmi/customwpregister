# customwpregister
WordPress a de nombreuses tâches d'enregistrement. WP Register facilite l'enregistrement des blocs personnalisés, des tailles d'images, des menus, des types d'articles, des taxonomies, des barres latérales et des widgets. 

## Utilisation
Incluez la classe Customwpregister dans votre plugin, votre thème ou votre thème enfant. Exigez-la dans votre fichier, utilisez un autoloader ou incluez-la en utilisant composer. Vous pouvez en savoir plus sur l'autoloading dans [le readme de wp-autoload](https://github.com/ahmedguesmi/wp-autoload).

### Construire votre tableau avec des enregistrements
Vous pouvez ajouter les types que vous souhaitez enregistrer dans un tableau multidimensionnel, comme expliqué dans l'exemple ci-dessous

```php
$registrations = [
    'blocks' => [
        [
            'type'  => 'custom/block-type',                     // Le type, l'objet ou le chemin json pour le bloc gutenberg personnalisé
            'args'  => ['style' => 'custom-block-type-style']   // Les arguments pour l'enregistrement d'un bloc, suivant les arguments du codex
        ]
    ]
    'image_sizes' => [
        [
            'name'   => 'fhd',
            'height' => 1080,
            'width'  => 1920,
            'crop'   => true
        ]
    ],
    'menus' => [
        'menu-location'     => __('Custom Menu Location', 'textdomain'),
        'another-location'  => __('AnotherCustom Menu Location', 'textdomain')
    ],     
    'post_types' => [
        [
            'name'          => 'beer', 
            'plural'        => __('Beers', 'textdomain'), 
            'singular'      => __('Beer', 'textdomain'), 
            'args'          => ['public' => true]       // Contient les arguments tels qu'ils sont pris en charge par register_post_type. (optionnel)
            'taxonomies'    => ['category']             // Contient les arguments tels qu'ils sont pris en charge par register_post_type. (optionnel)
            'slug'          => 'slug'                   // Connecte les taxonomies existantes à ce type de message. Doit être un tableau. (optionnel)
            'icon'          => 'dashicon-beer'          // Définit une icône de menu personnalisée pour wp-admin, avance rapide pour le paramètre menu_icon dans les arguments
        ]
    ],
    'sidebars' => [
        [
            'id'            => 'custom-sidebar', 
            'name'          => __('Custom Sidebar', 'textdomain'), 
            'description'   => __('Description for this sidebar', 'textdomain'),
            'before_widget' => '<section id="%1$s" class="widget %2$s">', // L'élément d'ouverture du widget (facultatif)
            'after_widget'  => '</section>',  // L'élément de fermeture du widget (facultatif)
            'before_title'  => '<h3 class="widget-title">',  // Le titre d'ouverture du widget (facultatif)
            'after_title'   => '</h3>' // La balise de fermeture du widget (facultatif)
        ]
    ],    
    'taxonomies' => [
        [
            'name'      => 'type', 
            'object'    => 'beer', 
            'plural'    => __('Types', 'textdomain'), 
            'singular'  => __('Type', 'textdomain'),
            'args'      => ['hierarchical' => true] // Contient les arguments tels qu'ils sont pris en charge par register_post_type. (optionnel)
       ]
    ],
    'widgets' => [
        'WidgetClass' // Le nom de votre classe de widget personnalisé, spécifié par le nom si vous utilisez l'autoload.
    ],
];
```
    
### Créer une instance
Créez une nouvelle instance de la classe Customwpregister avec votre tableau d'enregistrement et la chaîne textdomain comme arguments de la manière suivante.

```php
$register = new Ahmedguesmi\Customwpregister\Register( $registrations, 'textdomain' ) ;
```

La classe Register accepte deux arguments, à savoir un ``Array $registrations`` et une ``Chaîne $textdomain``.