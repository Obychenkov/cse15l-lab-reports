# Week 5 Lab Report: Researching Commands - Grep

## Option 1: -R (Recursive search) 
[Source](https://linuxhint.com/use-grep-recursively/)

The way `grep` normally works is it requires a file to be given, and returns all the lines that contain the given string. For example, if I wanted to find the string 'Volcano' in the file HandRHawaii.txt, I would run the following:
```
grep 'Volcano' travel_guides/berlitz1/HandRHawaii.txt
```
which would give the output
```
Chalet Kilauea $$–$$$ P.O. Box 998, Volcano, HI 96785; Tel.
of bed & breakfast accommodations in the Volcano area. They have
```

However, let's say I need to find the word 'Volcano', but I don't know what file or even folder it's in. That's where the `-R` option comes in handy as it does a recursive search through all the directories and subdirectories of the current working directory and prints out all of the files and lines containing that string, not just from one specific file. 

### Example 1
Going back to the volcano example, if I was to run 
```
grep -R 'Volcano'
```
I would get the output
```
travel_guides/berlitz1/HandRHawaii.txt:        Chalet Kilauea $$–$$$ P.O. Box 998, Volcano, HI 96785; Tel.
travel_guides/berlitz1/HandRHawaii.txt:        of bed & breakfast accommodations in the Volcano area. They have
travel_guides/berlitz1/IntroFWI.txt:        steep hills and rolling plains. Volcanoes, hummingbirds, mangroves,
travel_guides/berlitz1/WhereToFWI.txt:        Vacillating Volcano
travel_guides/berlitz1/WhereToFWI.txt:        Saint-Pierre and the Volcano
travel_guides/berlitz1/WhereToHawaii.txt:        Volcanoes National Park has active lava flows flowing to
travel_guides/berlitz2/CanaryIslands-WhereToGo.txt:The inland route south to Puerto del Rosario follows the FV-101 and a 
diversion, west along the FV-109 will bring you first to the Zoo Safari Calderón Hondo. There you can opt for either a 
half-hour camel trip or a 11⁄2 hour safari to the lunar landscape of the Volcano Calderón Hondo. Next comes the 
lace-making town of Lajares. And if you really want to get away from it all, continue on to El Cotillo. 
This tiny fishing village on the east coast also boasts some excellent beaches wonderful for windsurfing, 
plus a handful of local bars and some basic restaurants. Heading back south from El Cotillo, the FV-10 
rejoins the FV-101 at the small town of La Oliva. This is not especially 
attractive but it does feature two places of interest. Just off the main road stands the Casa de los 
Coroneles (House of the Colonels). Its name derives from its 18th-century tenants who once ruled the island. 
The decaying, cream-colored building still exudes a certain haughty, if melancholy, grandeur. By contrast, the 
nearby Centro de Arte Canario is bright and modern, exhibiting the works of some of the finest living Canarian artists.
```

As you might notice, I got the same two results from HandRHawaii.txt as if I ran `grep` without `-R`, but also results from numerous other files and even results from the berlitz2 subdirectory. Now I know what files to look into if I am looking for information on volcanoes.

### Example 2
```
grep -R 'Bob'
```
Gives the output
```
non-fiction/OUP/Berk/ch1.txt:•Bob and Sharon, parents of a 4-year-old: Our daughter, Lydia, could recite her ABCs and count from 1 to 20 by age 2 1/2. When we looked for a preschool, many programs appeared to do little more than let children play, so we chose one with lots of emphasis on academics. To me, Lydia’s preschool seems like great preparation for kindergarten and ﬁrst grade, but each morning, Lydia hates to go. Why is Lydia, who’s always been an upbeat, curious child, so unhappy?
travel_guides/berlitz1/HandRJamaica.txt:        district of New Kingston and the Bob Marley Museum. Each room in this
travel_guides/berlitz1/WhatToJamaica.txt:        and yellow colors that represent nature, blood, and sunshine. The Bob
travel_guides/berlitz1/WhatToJamaica.txt:        compound where singer and staunch Rastafarian Bob Marley lived and
travel_guides/berlitz1/WhatToJamaica.txt:        Bob Marley Museum and carefully managed by the Marley family to protect
travel_guides/berlitz1/WhereToEdinburgh.txt:        “Greyfriars Bobby” (see page 57). Behind Huntly House is Acheson House,
travel_guides/berlitz1/WhereToEdinburgh.txt:        of Greyfriars Bobby, just beside the main entrance. From here you can
travel_guides/berlitz1/WhereToItaly.txt:        holm oaks of the palace’s Boboli Gardens, a favorite picnic destination
travel_guides/berlitz1/WhereToItaly.txt:        one of the Boboli’s gardeners.
travel_guides/berlitz1/WhereToLakeDistrict.txt:        Newby Mill near Lakeside Stott Park, Bobbin Mill was still operating
travel_guides/berlitz2/Bali-History.txt:The public in the Netherlands was appalled by these grisly events. From then on, Bali and the Balinese came to be looked on as unique — to be protected from the colonial treatment that had turned the other islands into plantations exploited for profit. Tourism was discouraged although a few foreigners did make the journey and returned to the outside world with news of the island’s extraordinary culture... An American couple, Bob and Louise Koke, opened the first hotel on Kuta Beach in 1936; Louise G. Koke’s memoir, Our Hotel In Bali, provides an idyllic portrait of Bali’s first, tenuous endeavor at tourism from 1936 until the Japanese invasion in 1942.
travel_guides/berlitz2/Boston-WhereToGo.txt:Nearby, on the downtown side of the river, the new temple of this sport- crazy town rises beside North Station. In 1995 FleetCenter replaced the old Boston Garden where fans had cheered on such legends as Bobby Orr of the Boston Bruins and Larry Bird of the Celtics. Tours are given of the new facility.
travel_guides/berlitz2/Budapest-WhatToDo.txt:For more useful ideas, look in the bookshops for Budapest for Children by Bob Dent. If you would like a copy before you leave home, write to: The Budapest Sun, 1068 Budapest, Dózsa György út 84a.
travel_guides/berlitz2/California-History.txt:Black radicalism accelerated after the Watts riots in Los Angeles in 1965 and reached its peak with the Black Panthers in Oakland, a paramilitary organization led by Huey Newton, Eldridge Cleaver, and Bobby Seale. The Watts riots were sinisterly echoed in the Los Angeles riots of 1992, when the same area of South-Central L.A. was ravaged by violence in response to the acquittal of white police officers who were captured on videotape beating a black resident.
travel_guides/berlitz2/California-WhatToDo.txt:Big events in the California sporting calendar include the Bob Hope Desert Golf Classic at Palm Springs (February); the Long Beach Grand Prix in L.A. (March); the L.A. Marathon (March); and the San Francisco Marathon (July).
```

The working directory is written_2, with subdirectories non-fiction and travel_guides. This grep found results from a txt file in non-fiction as well as travel_guides and both of its subdirectories berlitz1 and berlitz2. This option by itself doesn't immediately give you all the information you need, however it gives you the files that include the information and a brief segment of the information to help you decide whether it's relevant to you or not. So the `-R` recursive search method is useful if you have multiple directories and/or files and you're unsure which ones have the information you need.

## Option 2: -i (Case insensitive) 
[Source](https://en.wikibooks.org/wiki/Grep)

Let's go back to the basic `grep` command and output as shown in Option 1:
```
grep 'Volcano' travel_guides/berlitz1/HandRHawaii.txt
```
Result:
```
Chalet Kilauea $$–$$$ P.O. Box 998, Volcano, HI 96785; Tel.
of bed & breakfast accommodations in the Volcano area. They have
```

However, here's the same basic grep command ran with a very small change of searching for `'volcano'` instead of `'Volcano'`
```
grep 'volcano' travel_guides/berlitz1/HandRHawaii.txt
```
Result:
```
<www.volcano-hawaii.com>. Brian and Lisha Crawford are the kings
```

Entirely different output that doesn't include the first result we saw. This might often be an issue because if I am looking for a specific word, whether it's capitalized or not can depend on a variety of factors such as if its at the start of a sentence or not, part of a url, or if it's a variable it'll differ based on what case the programmer chose to use. Sometimes, you just want to look for a string without caring about specific capitalization, and that's where the `-i` option comes in. Instead of looking for that specific string, `grep` will instead look for all the lower and upper case combinations of that string. Let's try it with the same volcanoes example:

### Example 1
```
grep -i 'Volcano' travel_guides/berlitz1/HandRHawaii.txt
```
Result:
```
Chalet Kilauea $$–$$$ P.O. Box 998, Volcano, HI 96785; Tel.
<www.volcano-hawaii.com>. Brian and Lisha Crawford are the kings
of bed & breakfast accommodations in the Volcano area. They have
```

As you can see, I get the results of the first and the second `grep` just by adding `-i`. Since I am just looking for any information about volcanoes, it doesn't matter what form they are in, so this option gives more results.

### Example 2

Here's another example, let's say I want to find out about wars in the history of Italy
```
grep -i ' war ' travel_guides/berlitz1/HistoryItaly.txt
```
*Side note: the string I'm search for is actually ' war ' with space characters on both sides. That's because despite ignoring case, `grep` still searches for the exact combination of characters, which means if I searched for 'war' words like 'forward', 'toward' and so on would also be counted, which isn't my intention.*

Result:
```
participated only by tax contributions to the war effort and minor
Italian supporters. The Third and final Punic War ended in 149 b.c. ,
This led to civil war and the despotic rule of Octavian, nephew and
participation in the ruinous Chioggia War on the Venetian lagoon
When the dust of war settled, it was the dazzling cultural
Italian treasuries, used to support their war effort and the Bonaparte
They were less amusing when hailing World War I as the
be “sacro egoismo,” Italy signed a secret treaty to enter the war on
petit bourgeois, war in uniform was their first real experience of
was denied knowledge of the secret war treaty until the Peace
during World War II.
of the Italian Empire. Italian war planes joined Hitler’s Luftwaffe on
General Franco’s side in the Spanish Civil War (5,000 Italian
France’s collapse in June 1940, plunged with Germany into World War II.
•1940Italy joins Nazi Germany in World War II
```

This finds lines with both 'War' and 'war'. War as often capitalized when used as part of a name of a historical event such as 'Punic War' or 'World War II', but is all lowercase when used as a word in a sentence. Therefore, `-i` helps ensure that all mentions of war are accounted for regardless of how they are used.

## Option 3: -l (Only matching files)
[Source](https://en.wikibooks.org/wiki/Grep)

In option 1 `-R` you might have noticed that the outputs are really lengthy at times and might seem too crowded to extract useful information out of them. This is where `-l` is useful, as it changes the grep output to only output the paths to files that contain that string, excluding the lines. 

As a note, this is really only useful with `-R` or other commands that allow `grep` to search multiple files, as by default `grep` is used on only one file, so the output of `-l` by itself would just be the path to the file that you already gave `grep`, which isn't incredibly useful.

### Example 1

I am once again looking for information on volcanoes, but I just want to see which files might be useful and don't want any other text printed to improve readability, I run
```
grep -Rl 'Volcano'
```
Result:
```
travel_guides/berlitz1/HandRHawaii.txt
travel_guides/berlitz1/IntroFWI.txt
travel_guides/berlitz1/WhereToFWI.txt
travel_guides/berlitz1/WhereToHawaii.txt
travel_guides/berlitz2/CanaryIslands-WhereToGo.txt
```

Nice, short, simple, easy to read paths. Now I can open or `grep` those files individually to see if they are useful instead of having to find the paths among the mess of text that just `-R` might output.

### Example 2
I really enjoyed learning about war in the history of Italy, I wonder what other countries had wars that I might want to read about from the same set of files:
```
grep -Rl ' war ' travel_guides/berlitz1
```
Result:
```
travel_guides/berlitz1/HistoryDublin.txt
travel_guides/berlitz1/HistoryEdinburgh.txt
travel_guides/berlitz1/HistoryEgypt.txt
travel_guides/berlitz1/HistoryFrance.txt
travel_guides/berlitz1/HistoryFWI.txt
travel_guides/berlitz1/HistoryGreek.txt
travel_guides/berlitz1/HistoryHawaii.txt
travel_guides/berlitz1/HistoryHongKong.txt
travel_guides/berlitz1/HistoryIndia.txt
travel_guides/berlitz1/HistoryIsrael.txt
travel_guides/berlitz1/HistoryIstanbul.txt
travel_guides/berlitz1/HistoryItaly.txt
travel_guides/berlitz1/HistoryJamaica.txt
travel_guides/berlitz1/HistoryJapan.txt
travel_guides/berlitz1/HistoryJerusalem.txt
travel_guides/berlitz1/HistoryLasVegas.txt
travel_guides/berlitz1/HistoryMadrid.txt
travel_guides/berlitz1/HistoryMalaysia.txt
travel_guides/berlitz1/HistoryMallorca.txt
travel_guides/berlitz1/IntroJapan.txt
travel_guides/berlitz1/WhereToEgypt.txt
travel_guides/berlitz1/WhereToFrance.txt
travel_guides/berlitz1/WhereToFWI.txt
travel_guides/berlitz1/WhereToGreek.txt
travel_guides/berlitz1/WhereToHongKong.txt
travel_guides/berlitz1/WhereToIbiza.txt
travel_guides/berlitz1/WhereToIndia.txt
travel_guides/berlitz1/WhereToIsrael.txt
travel_guides/berlitz1/WhereToIstanbul.txt
travel_guides/berlitz1/WhereToItaly.txt
travel_guides/berlitz1/WhereToJapan.txt
travel_guides/berlitz1/WhereToMadrid.txt
travel_guides/berlitz1/WhereToMalaysia.txt
```

Just to demonstrate a point, here's what the output would've looked like if the same command was ran without `-l`

```
travel_guides/berlitz1/HistoryDublin.txt:        however, civil war broke out between the supporters of Michael Collins
travel_guides/berlitz1/HistoryDublin.txt:        followers. The civil war lasted a year. In 1922 the new Irish Free
travel_guides/berlitz1/HistoryEdinburgh.txt:        went to war with France in 1294 and summoned John along with other
travel_guides/berlitz1/HistoryEdinburgh.txt:        resumed, aggravated by civil war at home as Edward Balliol (son of
travel_guides/berlitz1/HistoryEdinburgh.txt:        Parliamentarians in the civil war that had erupted across the border.
travel_guides/berlitz1/HistoryEgypt.txt:        powerful, twice declaring war on his sovereign and almost beating the
travel_guides/berlitz1/HistoryFrance.txt:        During war and peace alike in this feudal age, the Church and the
travel_guides/berlitz1/HistoryFrance.txt:        year later, France was once again at war with Germany.
travel_guides/berlitz1/HistoryFrance.txt:        brought the war to an end with Algerian independence in 1962. His major
travel_guides/berlitz1/HistoryFWI.txt:        With the war monopolizing shipping, the FWI suffered great economic
travel_guides/berlitz1/HistoryGreek.txt:        In 431 b.c. , Athens began a war with its neighbor and
travel_guides/berlitz1/HistoryGreek.txt:        war went on they could see that Athens was slowly losing its power.
travel_guides/berlitz1/HistoryGreek.txt:        Before the end of the war in 401 b.c. , many islands had already
travel_guides/berlitz1/HistoryGreek.txt:        rather than by historical geographical boundaries), declaring war on
travel_guides/berlitz1/HistoryGreek.txt:        Turks lost a short war with Italy, and were forced to relinquish the
travel_guides/berlitz1/HistoryGreek.txt:        As the Balkans flared to war once again, Greek nationalism
travel_guides/berlitz1/HistoryHawaii.txt:        The war broke out in Hawaii as nowhere else in America with
travel_guides/berlitz1/HistoryHawaii.txt:        war on Japan. Hawaii, as America’s western outpost and major Pacific
travel_guides/berlitz1/HistoryHongKong.txt:        China’s civil war sent distressing echoes to Hong Kong.
travel_guides/berlitz1/HistoryIndia.txt:        cultivated agriculture in the Punjab after waging war against the
travel_guides/berlitz1/HistoryIndia.txt:        Sikhs had been killing each other in war for many centuries.
travel_guides/berlitz1/HistoryIsrael.txt:        Israel was proclaimed. Immediately the first Israel-Arab war erupted,
travel_guides/berlitz1/HistoryIsrael.txt:        Jordan, Iraq, Lebanon, and Syria. After a year of war the UN interceded
travel_guides/berlitz1/HistoryIsrael.txt:        Egypt, Syria, Jordan, and Iraq with a preemptive strike. The war was
travel_guides/berlitz1/HistoryIstanbul.txt:        and was brought to the brink of civil war by the Iconoclastic Crisis,
travel_guides/berlitz1/HistoryIstanbul.txt:        risen from the status of war hero to become the lead­­er of the Turkish
travel_guides/berlitz1/HistoryIstanbul.txt:        when it entered the war on the side of the Allies. It joined NATO in
travel_guides/berlitz1/HistoryItaly.txt:        participated only by tax contributions to the war effort and minor
travel_guides/berlitz1/HistoryItaly.txt:        This led to civil war and the despotic rule of Octavian, nephew and
travel_guides/berlitz1/HistoryItaly.txt:        When the dust of war settled, it was the dazzling cultural
travel_guides/berlitz1/HistoryItaly.txt:        Italian treasuries, used to support their war effort and the Bonaparte
travel_guides/berlitz1/HistoryItaly.txt:        be “sacro egoismo,” Italy signed a secret treaty to enter the war on
travel_guides/berlitz1/HistoryItaly.txt:        petit bourgeois, war in uniform was their first real experience of
travel_guides/berlitz1/HistoryJapan.txt:        confrontation with the West. Japan hoped that war in Europe would
travel_guides/berlitz1/HistoryJapan.txt:        radio broadcast, announcing that “the war situation has developed not
travel_guides/berlitz1/HistoryJapan.txt:        then two decades after the war had left the country in ruins.
travel_guides/berlitz1/HistoryJerusalem.txt:        constructing the Temple because he was a man of war with blood on his
travel_guides/berlitz1/HistoryLasVegas.txt:        as a result of America’s war effort. By 1945, the population had grown
travel_guides/berlitz1/HistoryMadrid.txt:        II. The subsequent war over Spanish succession resulted in the
travel_guides/berlitz1/HistoryMadrid.txt:        rightful throne in the Royal Palace of Madrid in 1814. But the war and
travel_guides/berlitz1/HistoryMadrid.txt:        civil war developed into one of the great causes of the 20th century,
travel_guides/berlitz1/HistoryMadrid.txt:        Europeans saw the civil war as a crucial conflict between democracy and
travel_guides/berlitz1/HistoryMadrid.txt:        The war was brutal and bloody, and both sides committed
travel_guides/berlitz1/HistoryMadrid.txt:        Even when the war ended, the hardship continued. Despite
travel_guides/berlitz1/HistoryMalaysia.txt:        If Japanese treatment of Allied prisoners of war in Malaya
travel_guides/berlitz1/HistoryMalaysia.txt:        victims in a guerrilla war launched from jungle enclaves by communist
travel_guides/berlitz1/HistoryMallorca.txt:        claimant — and retained it when the war was over. In 1708 Britain
travel_guides/berlitz1/HistoryMallorca.txt:        arrived to fight on the side of the Republicans. The war lasted three
travel_guides/berlitz1/IntroJapan.txt:        Asia during the war remains a stumbling block to “normal” international
travel_guides/berlitz1/IntroJapan.txt:        blatantly manipulated the concept to prepare the country for war and
travel_guides/berlitz1/WhereToEgypt.txt:        Nile, and weapons of war including spears and shields. Two harpists
travel_guides/berlitz1/WhereToFrance.txt:        Guerre, a museum that gives an excellent overview of the war and the
travel_guides/berlitz1/WhereToFrance.txt:        devastations of war and the more-recent depression of the region’s
travel_guides/berlitz1/WhereToFWI.txt:        lower reaches, relics and documents relating to the war were kept in a
travel_guides/berlitz1/WhereToGreek.txt:        original — little damaged either by war or earthquakes. Its gray-tiled
travel_guides/berlitz1/WhereToHongKong.txt:        ceiling, a popular spot dedicated to the Taoist gods of war and
travel_guides/berlitz1/WhereToIbiza.txt:        against the Americans in the war of 1898.
travel_guides/berlitz1/WhereToIndia.txt:        Gate, the war memorial designed by Lutyens in the style of a triumphal
travel_guides/berlitz1/WhereToIndia.txt:        of these trekkers were British troops returning from the war with the
travel_guides/berlitz1/WhereToIsrael.txt:        became synonymous with war and destruction. It was here that British
travel_guides/berlitz1/WhereToIstanbul.txt:        and Turkish armies. Each war cemetery is signposted, and all are
travel_guides/berlitz1/WhereToItaly.txt:        war captives, and (according to some historians) Christians.
travel_guides/berlitz1/WhereToJapan.txt:        and the Yushukan museum of war memorabilia.
travel_guides/berlitz1/WhereToJapan.txt:        horror of atomic weapons and nuclear war in general, driving toward the
travel_guides/berlitz1/WhereToMadrid.txt:        rebuilt after civil war destruction. The Plaza de Zocodover is where
travel_guides/berlitz1/WhereToMalaysia.txt:        Police Museum (1961) on Jalan Semarak highlights the war against the
travel_guides/berlitz1/WhereToMalaysia.txt:        stairs you’ll find an old fort which was used in a local civil war in
travel_guides/berlitz1/WhereToMalaysia.txt:        center for Japanese prisoners of war during World War II. It is now the
travel_guides/berlitz1/WhereToMalaysia.txt:        from the ashes of the war after allied bombing razed the city during
travel_guides/berlitz1/WhereToMalaysia.txt:        Other links to the war years include the Australian
travel_guides/berlitz1/WhereToMalaysia.txt:        Memorial on the site of the former prisoner of war in Taman Rimba, off
```

Still readable, but another aspect of `-l` is that it guarantees that each file is listed once. You might notice that this output is lengthier because each time the word war comes up in the file, it will be printed on a separate line, resulting in multiple of the same file path being printed out which once again just clumps up the screen with information that might not be necessary to someone just looking for the relevant files.

## Option 4: -c (Number of matching lines) 
[Source](https://en.wikibooks.org/wiki/Grep)

Say you are the author of HistoryItaly.txt. You're worried that you talked about war too much, so you want to check in how many lines the word war appears. This can be done with the `-c` option, which instead of outputting the lines themselves simply outputs one integer which states how many lines would've been printed by `grep`.

### Example 1
```
grep -c ' war ' travel_guides/berlitz1/HistoryItaly.txt 
```
Result:
```
8
```

Only 8 lines match war so now as the author you know you didn't talk about war too much and likely gave a balanced recount of the history of Italy without just focusing on warfare, good work!

### Example 2

Here's another scenario: You are a student given the entirety of the travel_guides directory and told to pick one place and write an essay analyzing its history related to war. You haven't read any of the files yet, how do you figure out which place to write about or at least where to start your search? Let's use 3 of the options described with a focus on `-c`.
```
grep -Ric ' war ' travel_guides
```
Result: 
```
travel_guides/berlitz1/HandRHawaii.txt:0
travel_guides/berlitz1/HandRHongKong.txt:0
travel_guides/berlitz1/HandRIbiza.txt:0
travel_guides/berlitz1/HandRIsrael.txt:0
travel_guides/berlitz1/HandRIstanbul.txt:0
travel_guides/berlitz1/HandRJamaica.txt:0
travel_guides/berlitz1/HandRJerusalem.txt:0
travel_guides/berlitz1/HandRLakeDistrict.txt:0
travel_guides/berlitz1/HandRLasVegas.txt:0
travel_guides/berlitz1/HandRLisbon.txt:0
travel_guides/berlitz1/HandRLosAngeles.txt:0
travel_guides/berlitz1/HandRMadeira.txt:0
travel_guides/berlitz1/HandRMadrid.txt:0
travel_guides/berlitz1/HandRMallorca.txt:0
travel_guides/berlitz1/HistoryDublin.txt:5
travel_guides/berlitz1/HistoryEdinburgh.txt:3
travel_guides/berlitz1/HistoryEgypt.txt:3
travel_guides/berlitz1/HistoryFrance.txt:8
travel_guides/berlitz1/HistoryFWI.txt:4
travel_guides/berlitz1/HistoryGreek.txt:8
travel_guides/berlitz1/HistoryHawaii.txt:4
travel_guides/berlitz1/HistoryHongKong.txt:3
travel_guides/berlitz1/HistoryIbiza.txt:3
travel_guides/berlitz1/HistoryIndia.txt:5
travel_guides/berlitz1/HistoryIsrael.txt:7
travel_guides/berlitz1/HistoryIstanbul.txt:8
travel_guides/berlitz1/HistoryItaly.txt:15
travel_guides/berlitz1/HistoryJamaica.txt:4
travel_guides/berlitz1/HistoryJapan.txt:10
travel_guides/berlitz1/HistoryJerusalem.txt:3
travel_guides/berlitz1/HistoryLakeDistrict.txt:0
travel_guides/berlitz1/HistoryLasVegas.txt:2
travel_guides/berlitz1/HistoryMadeira.txt:2
travel_guides/berlitz1/HistoryMadrid.txt:11
travel_guides/berlitz1/HistoryMalaysia.txt:5
travel_guides/berlitz1/HistoryMallorca.txt:7
travel_guides/berlitz1/IntroDublin.txt:0
travel_guides/berlitz1/IntroEdinburgh.txt:0
travel_guides/berlitz1/IntroEgypt.txt:0
travel_guides/berlitz1/IntroFrance.txt:0
travel_guides/berlitz1/IntroFWI.txt:0
travel_guides/berlitz1/IntroGreek.txt:0
travel_guides/berlitz1/IntroHongKong.txt:0
travel_guides/berlitz1/IntroIbiza.txt:0
travel_guides/berlitz1/IntroIndia.txt:0
travel_guides/berlitz1/IntroIsrael.txt:0
travel_guides/berlitz1/IntroIstanbul.txt:0
travel_guides/berlitz1/IntroItaly.txt:0
travel_guides/berlitz1/IntroJamaica.txt:0
travel_guides/berlitz1/IntroJapan.txt:3
travel_guides/berlitz1/IntroJerusalem.txt:1
travel_guides/berlitz1/IntroLakeDistrict.txt:0
travel_guides/berlitz1/IntroLasVegas.txt:0
travel_guides/berlitz1/IntroLosAngeles.txt:0
travel_guides/berlitz1/IntroMadeira.txt:0
travel_guides/berlitz1/IntroMadrid.txt:1
travel_guides/berlitz1/IntroMalaysia.txt:0
travel_guides/berlitz1/IntroMallorca.txt:0
travel_guides/berlitz1/JungleMalaysia.txt:0
travel_guides/berlitz1/WhatToDublin.txt:0
travel_guides/berlitz1/WhatToEdinburgh.txt:0
travel_guides/berlitz1/WhatToEgypt.txt:0
travel_guides/berlitz1/WhatToFrance.txt:0
travel_guides/berlitz1/WhatToFWI.txt:0
travel_guides/berlitz1/WhatToGreek.txt:1
travel_guides/berlitz1/WhatToHawaii.txt:1
travel_guides/berlitz1/WhatToHongKong.txt:0
travel_guides/berlitz1/WhatToIbiza.txt:0
travel_guides/berlitz1/WhatToIndia.txt:0
travel_guides/berlitz1/WhatToIsrael.txt:0
travel_guides/berlitz1/WhatToIstanbul.txt:0
travel_guides/berlitz1/WhatToItaly.txt:0
travel_guides/berlitz1/WhatToJamaica.txt:1
travel_guides/berlitz1/WhatToJapan.txt:0
travel_guides/berlitz1/WhatToLakeDistrict.txt:0
travel_guides/berlitz1/WhatToLasVegas.txt:0
travel_guides/berlitz1/WhatToLosAngeles.txt:0
travel_guides/berlitz1/WhatToMadeira.txt:0
travel_guides/berlitz1/WhatToMalaysia.txt:0
travel_guides/berlitz1/WhatToMallorca.txt:0
travel_guides/berlitz1/WhereToDublin.txt:3
travel_guides/berlitz1/WhereToEdinburgh.txt:4
travel_guides/berlitz1/WhereToEgypt.txt:1
travel_guides/berlitz1/WhereToFrance.txt:9
travel_guides/berlitz1/WhereToFWI.txt:1
travel_guides/berlitz1/WhereToGreek.txt:4
travel_guides/berlitz1/WhereToHawaii.txt:1
travel_guides/berlitz1/WhereToHongKong.txt:5
travel_guides/berlitz1/WhereToIbiza.txt:1
travel_guides/berlitz1/WhereToIndia.txt:3
travel_guides/berlitz1/WhereToIsrael.txt:4
travel_guides/berlitz1/WhereToIstanbul.txt:5
travel_guides/berlitz1/WhereToItaly.txt:2
travel_guides/berlitz1/WhereToJapan.txt:14
travel_guides/berlitz1/WhereToJerusalem.txt:2
travel_guides/berlitz1/WhereToLakeDistrict.txt:1
travel_guides/berlitz1/WhereToLosAngeles.txt:1
travel_guides/berlitz1/WhereToMadeira.txt:2
travel_guides/berlitz1/WhereToMadrid.txt:4
travel_guides/berlitz1/WhereToMalaysia.txt:22
travel_guides/berlitz1/WhereToMallorca.txt:2
travel_guides/berlitz2/Algarve-History.txt:4
travel_guides/berlitz2/Algarve-Intro.txt:0
travel_guides/berlitz2/Algarve-WhatToDo.txt:0
travel_guides/berlitz2/Algarve-WhereToGo.txt:0
travel_guides/berlitz2/Amsterdam-History.txt:2
travel_guides/berlitz2/Amsterdam-Intro.txt:0
travel_guides/berlitz2/Amsterdam-WhatToDo.txt:0
travel_guides/berlitz2/Amsterdam-WhereToGo.txt:3
travel_guides/berlitz2/Athens-History.txt:6
travel_guides/berlitz2/Athens-Intro.txt:0
travel_guides/berlitz2/Athens-WhatToDo.txt:0
travel_guides/berlitz2/Athens-WhereToGo.txt:3
travel_guides/berlitz2/Bahamas-History.txt:8
travel_guides/berlitz2/Bahamas-Intro.txt:1
travel_guides/berlitz2/Bahamas-WhatToDo.txt:0
travel_guides/berlitz2/Bahamas-WhereToGo.txt:2
travel_guides/berlitz2/Bali-History.txt:3
travel_guides/berlitz2/Bali-WhatToDo.txt:0
travel_guides/berlitz2/Bali-WhereToGo.txt:3
travel_guides/berlitz2/Barcelona-History.txt:3
travel_guides/berlitz2/Barcelona-WhatToDo.txt:0
travel_guides/berlitz2/Barcelona-WhereToGo.txt:1
travel_guides/berlitz2/Beijing-History.txt:3
travel_guides/berlitz2/Beijing-WhatToDo.txt:0
travel_guides/berlitz2/Beijing-WhereToGo.txt:0
travel_guides/berlitz2/Berlin-History.txt:8
travel_guides/berlitz2/Berlin-WhatToDo.txt:1
travel_guides/berlitz2/Berlin-WhereToGo.txt:13
travel_guides/berlitz2/Bermuda-history.txt:4
travel_guides/berlitz2/Bermuda-WhatToDo.txt:0
travel_guides/berlitz2/Bermuda-WhereToGo.txt:6
travel_guides/berlitz2/Boston-WhereToGo.txt:3
travel_guides/berlitz2/Budapest-History.txt:5
travel_guides/berlitz2/Budapest-WhatToDo.txt:0
travel_guides/berlitz2/Budapest-WhereoGo.txt:7
travel_guides/berlitz2/California-History.txt:2
travel_guides/berlitz2/California-WhatToDo.txt:0
travel_guides/berlitz2/California-WhereToGo.txt:1
travel_guides/berlitz2/Canada-History.txt:12
travel_guides/berlitz2/Canada-WhereToGo.txt:16
travel_guides/berlitz2/CanaryIslands-History.txt:4
travel_guides/berlitz2/CanaryIslands-WhatToDo.txt:0
travel_guides/berlitz2/CanaryIslands-WhereToGo.txt:0
travel_guides/berlitz2/Cancun-History.txt:1
travel_guides/berlitz2/Cancun-WhatToDo.txt:0
travel_guides/berlitz2/Cancun-WhereToGo.txt:4
travel_guides/berlitz2/China-History.txt:5
travel_guides/berlitz2/China-WhatToDo.txt:0
travel_guides/berlitz2/China-WhereToGo.txt:8
travel_guides/berlitz2/Costa-History.txt:7
travel_guides/berlitz2/Costa-WhatToDo.txt:0
travel_guides/berlitz2/Costa-WhereToGo.txt:2
travel_guides/berlitz2/CostaBlanca-History.txt:8
travel_guides/berlitz2/CostaBlanca-WhatToDo.txt:0
travel_guides/berlitz2/Crete-History.txt:5
travel_guides/berlitz2/Crete-WhatToDo.txt:0
travel_guides/berlitz2/Crete-WhereToGo.txt:2
travel_guides/berlitz2/CstaBlanca-WhereToGo.txt:6
travel_guides/berlitz2/Cuba-History.txt:2
travel_guides/berlitz2/Cuba-WhatToDo.txt:0
travel_guides/berlitz2/Cuba-WhereToGo.txt:4
travel_guides/berlitz2/Nepal-History.txt:0
travel_guides/berlitz2/Nepal-WhatToDo.txt:2
travel_guides/berlitz2/Nepal-WhereToGo.txt:0
travel_guides/berlitz2/NewOrleans-History.txt:9
travel_guides/berlitz2/Paris-WhatToDo.txt:0
travel_guides/berlitz2/Paris-WhereToGo.txt:1
travel_guides/berlitz2/Poland-History.txt:11
travel_guides/berlitz2/Poland-WhatToDo.txt:0
travel_guides/berlitz2/Portugal-History.txt:2
travel_guides/berlitz2/Portugal-WhatToDo.txt:0
travel_guides/berlitz2/Portugal-WhereToGo.txt:0
travel_guides/berlitz2/PuertoRico-History.txt:2
travel_guides/berlitz2/PuertoRico-WhatToDo.txt:0
travel_guides/berlitz2/PuertoRico-WhereToGo.txt:1
travel_guides/berlitz2/Vallarta-History.txt:1
travel_guides/berlitz2/Vallarta-WhatToDo.txt:0
travel_guides/berlitz2/Vallarta-WhereToGo.txt:0
```

What we did was search for ' war ' recursively in travel_guides regardless of case. 

Notice that `-c` combined with `-R` can actually make the output a bit longer because it will actually print out every single file in all the subdirectories even if it doesn't include any instances of that string. Of course, that can be avoided with additional specifications and regex, but I won't get into that. 

So how is this useful? Back to the imagined but very much real world scenario. I, as a student, can now look through just the numbers (I can sort the output too to make it easier, but once again not something I'll get into) to figure out which places might have had the most wars. After a quick visual scan, I might notice that Poland, Berlin, and Malasya all have a good amount of mentions of war, which means that they might be better candidates for my essay. So instead of counting the lines that would've been output by just `grep -Ri` and dealing with the visual clutter, I can very quickly and easily look at numbers and proceed based on that information.
