---
title: ABOUT
description: 永不放棄，才是世界的真理
date: 2020-12-13 18:07:28
type: "about"
---
```php
class DanielSung extends Person 
{
    private $name      = "Daniel Sung";
    private $mail      = "activearmy720@gmail.com";
    private $motto     = "Never Give Up!!";
    private $gender    = "Male";
    private $iving_now = "Taipei";
    private $skills    = [ "PHP", "Laravel", "MySQL", "JavaScript", "jQuery" ];
    private $learning  = [ "Vue.js" ];
    private $interest  = [ "BasketBall", "Movie", "Travel" ];

    public function getSkills() {
        return $this->skills;
    }

    public function Coding($lang) {
        echo $this->name . '就愛寫' . $lang . '~';
    }
}

$daniel_sung = new DanielSung;
$skills = $daniel_sung->getSkills();
foreach($skills as $skill)
{
    $daniel_sung->Coding($skill);
}
```