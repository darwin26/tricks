# Modul Minibeispiel - Kategorieliste mit getChildren()

- [Beschreibung](#beschreibung)
- [Moduleingabe](#moduleingabe)
- [Modulausgabe](#modulausgabe)

<a name="beschreibung"></a>
## Beschreibung

Ausgabe der Kategorien der aktuellen Ebene

<a name="moduleingabe"></a>
## Moduleingabe

    <div class="panel panel-primary">
        <div class="panel-heading"><i class="fa fa-question-circle" aria-hidden="true"></i> Kategorieliste</div>
        <div class="panel-body">
            Erstellt eine Liste aller Unterkategorien dieser Kategorie-Ebene
        </div>
    </div>
 

<a name="modulausgabe"></a>
## Modulausgabe

    <?php
    // Variablen setzen: 
    $catoutput = $cat = $cats = $catName = $catId = $catUrl = "";
    
    // Aktuelle Kategorie ermitteln
    $cat = rex_category::get($this->getValue('category_id'));
    
    // Kinder ermitteln
    $cats = $cat->getChildren();
    
    // Prüfen ob ein Ergebnis vorliegt
    if ($cats) {
        // Auslesen der Kategorien
        foreach ($cats as $cat) {
            if ($cat->isOnline()) {
                
                // ID ermitteln
                $catId = $cat->getId();
                
                // Name der Kategorie
                $catName = $cat->getName();
                
                // Url anhand ID ermitteln
                $catUrl =  rex_getUrl($catId);
                
                // Zwischenspeichern des Ergebnisses
                $catoutput .= '<li><a href="' . $catUrl . '">' . $catName . '<a></li>' . "\n";
            }
        }
        
        // Ausgabe 
        echo '<ul class="catlist">'.$catoutput.'</ul>';
        unset ($cats);
    }
    ?>