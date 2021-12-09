| ![](gifs/h-scroll/H-D.gif) | ![](gifs/h-scroll/H-o.gif) | ![](gifs/h-scroll/H-r.gif) | ![](gifs/h-scroll/H-k.gif) |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|
|  |  |   |  | ![](gifs/W.gif) | ![](gifs/o.gif) | ![](gifs/r.gif) | ![](gifs/d.gif) |  |  |  |  |
|  |  |  |  |  |  |  |  | ![](gifs/v-scroll/V-P.gif) | ![](gifs/v-scroll/V-l.gif) | ![](gifs/v-scroll/V-a.gif) | ![](gifs/v-scroll/V-y.gif) | 

<br>

imagemagick is massive, it's too big in fact but that doesn't mean we can't mess around with it and see what we can come up with, i'm interested in making small animated gifs of keyboard characters and that's exactly what i'm going to showcase here

note: there are a lot of little gifs need to be loaded for this page to look correctly, if you see any weird behavior of links not loading just refresh the page and your web browser hopefully caches everything by that time

this tutorial markdown was made possible partially by a helpful [comment on reddit](https://www.reddit.com/r/zsh/comments/r44ajo/need_help_converting_special_characters_in_file/) that fixed my problem printing speciall characters and helped giving usable names for them

<br>

### quick links
 * [output all characters](https://github.com/junguler/_dork-word-play#output-all-of-the-characters-in-a-for-loop)
 * [output special characters](https://github.com/junguler/_dork-word-play#printing-special-characters)
 * [animate the characters](https://github.com/junguler/_dork-word-play#animating-the-characters)
 * [animate the special characters](https://github.com/junguler/_dork-word-play#animating-special-characters)
 * [invert your gifs](https://github.com/junguler/_dork-word-play#invert-your-output-gifs)
 * [scroll your gifs](https://github.com/junguler/_dork-word-play#scroll-your-gifs)
 * [combine multiple filters](https://github.com/junguler/_dork-word-play#combine-multiple-filters)
 * [rotate your characters](https://github.com/junguler/_dork-word-play#rotate-your-characters)
 * [shades of grey as colors](https://github.com/junguler/_dork-word-play#using-shades-of-grey-as-color)
 * [merge multiple files together](https://github.com/junguler/_dork-word-play#merge-multiple-files-together)
 * [make a smooth gradient motion](https://github.com/junguler/_dork-word-play#making-a-smooth-gradient-animation-the-hard-way)
 * [variable sizes](https://github.com/junguler/_dork-word-play#variable-sizes)
 * [use multiple fonts](https://github.com/junguler/_dork-word-play#use-multiple-fonts)
 * [change character position](https://github.com/junguler/_dork-word-play#change-character-position)

<br>

## how to create an image using characters with imagemagick?
this couldn't be more easier, we'll use the program `convert` (in the newest versions it's called magick so if you don't have the convert commandline program just change convert to magick in the commands) to achieve this
```
convert -gravity center -background yellow -fill black -size 30x30 caption:"A" A.jpg
```
![A-A](temp/A-A.jpg)

as you can see `-gravity center` is supposed to center our character vertically and horizontally but it doesn't do that completely, we can correct this using `-trim` which removes white spaces in the image and pad it to center with `-extent` and passing the same size as our output image
```
convert -gravity center -background yellow -fill black -size 30x30 caption:"A" -trim -extent 30x30 A.jpg
```
![A-B](temp/A-B.jpg)

<br>

## output all of the characters in a for loop
now that we know how to output an image we'll use a for loop to convert all the numbers and alphabet characters in lower and higher case
```
for i in {a..z} {A..Z} {0..9} ; do convert -gravity center -trim -background yellow -fill black -font ./nerd.ttf -size 30x30 caption:$i -extent 30x30 $i.jpg ; done
```

![0](images/0.jpg)
![1](images/1.jpg)
![2](images/2.jpg)
![3](images/3.jpg)
![4](images/4.jpg)
![5](images/5.jpg)
![6](images/6.jpg)
![7](images/7.jpg)
![8](images/8.jpg)
![9](images/9.jpg)
![a](images/a.jpg)
![b](images/b.jpg)
![c](images/c.jpg)
![d](images/d.jpg)
![e](images/e.jpg)
![f](images/f.jpg)
![g](images/g.jpg)
![h](images/h.jpg)
![i](images/i.jpg)
![j](images/j.jpg)
![k](images/k.jpg)
![l](images/l.jpg)
![m](images/m.jpg)
![n](images/n.jpg)
![o](images/o.jpg)
![p](images/p.jpg)
![q](images/q.jpg)
![r](images/r.jpg)
![s](images/s.jpg)
![t](images/t.jpg)
![u](images/u.jpg)
![v](images/v.jpg)
![w](images/w.jpg)
![x](images/x.jpg)
![y](images/y.jpg)
![z](images/z.jpg)
![A](images/A.jpg)
![B](images/B.jpg)
![C](images/C.jpg)
![D](images/D.jpg)
![E](images/E.jpg)
![F](images/F.jpg)
![G](images/G.jpg)
![H](images/H.jpg)
![I](images/I.jpg)
![J](images/J.jpg)
![K](images/K.jpg)
![L](images/L.jpg)
![M](images/M.jpg)
![N](images/N.jpg)
![O](images/O.jpg)
![P](images/P.jpg)
![Q](images/Q.jpg)
![R](images/R.jpg)
![S](images/S.jpg)
![T](images/T.jpg)
![U](images/U.jpg)
![V](images/V.jpg)
![W](images/W.jpg)
![X](images/X.jpg)
![Y](images/Y.jpg)
![Z](images/Z.jpg)

`{a..z} {A..Z} {0..9}` in our for loop tells our shell to iterate thru numbers 0 to 9, characters from a to z and A to Z one by one

we also used a custom font with `-font` called `nerd.ttf` which was actually `Caskaydia Cove Nerd Font Mono` which i renamed for simplicity and put inside the folder i'm making these images, you can also pass the absolute path to it in your filesystem 

the mono in that font name refers to every character taking the same width as other, these fonts are typically used in ascii art, terminal emulators and code editors to easily be able to read them but i'm using the mono variant because it's easier to fit into the image

<br>

## printing special characters
special characters are harder to work with since they are not aloud to be used in file names in windows specially so because we want to have a cross-platform solution we convert their file names to their hex counterparts, note that this command is a zsh exclusive command and doesn't work on bash
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background yellow -fill black -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char $hex.jpg ; done
```

![21](images/21.jpg)
![22](images/22.jpg)
![23](images/23.jpg)
![24](images/24.jpg)
![25](images/25.jpg)
![26](images/26.jpg)
![27](images/27.jpg)
![28](images/28.jpg)
![29](images/29.jpg)
![2A](images/2A.jpg)
![2B](images/2B.jpg)
![2C](images/2C.jpg)
![2D](images/2D.jpg)
![2E](images/2E.jpg)
![2F](images/2F.jpg)
![3A](images/3A.jpg)
![3B](images/3B.jpg)
![3C](images/3C.jpg)
![3D](images/3D.jpg)
![3E](images/3E.jpg)
![3F](images/3F.jpg)
![40](images/40.jpg)
![5B](images/5B.jpg)
![5C](images/5C.jpg)
![5D](images/5D.jpg)
![5E](images/5E.jpg)
![60](images/60.jpg)
![7B](images/7B.jpg)
![7C](images/7C.jpg)
![7D](images/7D.jpg)
![7E](images/7E.jpg)

notice the segmented ranges in our for loop ``{\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~}`` the reason for this is that we don't want duplicate characters as our normal characters above so we exclude the ranges they are in within our for loop, if you don't care about file names you can do ``{\!..~}`` and combine both steps together

<br>

## animating the characters
so far we've been working with static image but let's change all of that and use ffmpeg to make a simple animation, we'll combine two for loops together one for the degrees of hue change (which changes the color of the images) and one for ffmpeg to iterate thru our images
```
for h in {30..360..30} ; for i in {a..z}.jpg {A..Z}.jpg {0..9}.jpg ; do mkdir output ; ffmpeg -i $i -vf hue=h=$h output/$h-$i ; done
```

we also made a `output` folder and put the output images inside it to keep things organized, now cd into that folder ``cd output/``

now we are ready to animate these image sequences using the `convert` program
```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -v *-$m.jpg) $m.gif ; done 
```
notice that the same pattern that we used when converting the input images is used for outputting the animations, we also used `ls -v` here to sort filenames numerically, if you don't do this the shell doesn't really sort filenames correctly and only sort by the first digit number, for example 20.jpg is placed earlier than 3.jpg

![0](gifs/0.gif)
![1](gifs/1.gif)
![2](gifs/2.gif)
![3](gifs/3.gif)
![4](gifs/4.gif)
![5](gifs/5.gif)
![6](gifs/6.gif)
![7](gifs/7.gif)
![8](gifs/8.gif)
![9](gifs/9.gif)
![a](gifs/a.gif)
![b](gifs/b.gif)
![c](gifs/c.gif)
![d](gifs/d.gif)
![e](gifs/e.gif)
![f](gifs/f.gif)
![g](gifs/g.gif)
![h](gifs/h.gif)
![i](gifs/i.gif)
![j](gifs/j.gif)
![k](gifs/k.gif)
![l](gifs/l.gif)
![m](gifs/m.gif)
![n](gifs/n.gif)
![o](gifs/o.gif)
![p](gifs/p.gif)
![q](gifs/q.gif)
![r](gifs/r.gif)
![s](gifs/s.gif)
![t](gifs/t.gif)
![u](gifs/u.gif)
![v](gifs/v.gif)
![w](gifs/w.gif)
![x](gifs/x.gif)
![y](gifs/y.gif)
![z](gifs/z.gif)
![A](gifs/A.gif)
![B](gifs/B.gif)
![C](gifs/C.gif)
![D](gifs/D.gif)
![E](gifs/E.gif)
![F](gifs/F.gif)
![G](gifs/G.gif)
![H](gifs/H.gif)
![I](gifs/I.gif)
![J](gifs/J.gif)
![K](gifs/K.gif)
![L](gifs/L.gif)
![M](gifs/M.gif)
![N](gifs/N.gif)
![O](gifs/O.gif)
![P](gifs/P.gif)
![Q](gifs/Q.gif)
![R](gifs/R.gif)
![S](gifs/S.gif)
![T](gifs/T.gif)
![U](gifs/U.gif)
![V](gifs/V.gif)
![W](gifs/W.gif)
![X](gifs/X.gif)
![Y](gifs/Y.gif)
![Z](gifs/Z.gif)

<br>

## animating special characters
the same principles applies here, we just need to adjust our commands a bit, first the ffmpeg command
```
for h in {30..360..30} ; for i in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do mkdir output2 ; ffmpeg -i $i.jpg -vf hue=h=$h output2/$h-$i.jpg ; done
```
because we only want specially characters and don't need duplicates we specially named every output file we need, we also made a new output2 folder to keep things organized, cd into the folder like before, now lets convert them to animated gifs
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -v *-$m.jpg) $m.gif ; done
```

![21](gifs/21.gif)
![22](gifs/22.gif)
![23](gifs/23.gif)
![24](gifs/24.gif)
![25](gifs/25.gif)
![26](gifs/26.gif)
![27](gifs/27.gif)
![28](gifs/28.gif)
![29](gifs/29.gif)
![2A](gifs/2A.gif)
![2B](gifs/2B.gif)
![2C](gifs/2C.gif)
![2D](gifs/2D.gif)
![2E](gifs/2E.gif)
![2F](gifs/2F.gif)
![3A](gifs/3A.gif)
![3B](gifs/3B.gif)
![3C](gifs/3C.gif)
![3D](gifs/3D.gif)
![3E](gifs/3E.gif)
![3F](gifs/3F.gif)
![40](gifs/40.gif)
![5B](gifs/5B.gif)
![5C](gifs/5C.gif)
![5D](gifs/5D.gif)
![5E](gifs/5E.gif)
![60](gifs/60.gif)
![7B](gifs/7B.gif)
![7C](gifs/7C.gif)
![7D](gifs/7D.gif)
![7E](gifs/7E.gif)

<br>

## invert your output gifs
the easiest way to modify our newly made gifs is to invert them, it really changes the look of everything and it's so simple to do

```
for i in *.gif ; do mkdir inverted ; ffmpeg -i $i -vf negate inverted/I-$i ; done
```

![I-0](gifs/inverted/I-0.gif)
![I-1](gifs/inverted/I-1.gif)
![I-2](gifs/inverted/I-2.gif)
![I-3](gifs/inverted/I-3.gif)
![I-4](gifs/inverted/I-4.gif)
![I-5](gifs/inverted/I-5.gif)
![I-6](gifs/inverted/I-6.gif)
![I-7](gifs/inverted/I-7.gif)
![I-8](gifs/inverted/I-8.gif)
![I-9](gifs/inverted/I-9.gif)
![I-21](gifs/inverted/I-21.gif)
![I-22](gifs/inverted/I-22.gif)
![I-23](gifs/inverted/I-23.gif)
![I-24](gifs/inverted/I-24.gif)
![I-25](gifs/inverted/I-25.gif)
![I-26](gifs/inverted/I-26.gif)
![I-27](gifs/inverted/I-27.gif)
![I-28](gifs/inverted/I-28.gif)
![I-29](gifs/inverted/I-29.gif)
![I-2A](gifs/inverted/I-2A.gif)
![I-2B](gifs/inverted/I-2B.gif)
![I-2C](gifs/inverted/I-2C.gif)
![I-2D](gifs/inverted/I-2D.gif)
![I-2E](gifs/inverted/I-2E.gif)
![I-2F](gifs/inverted/I-2F.gif)
![I-3A](gifs/inverted/I-3A.gif)
![I-3B](gifs/inverted/I-3B.gif)
![I-3C](gifs/inverted/I-3C.gif)
![I-3D](gifs/inverted/I-3D.gif)
![I-3E](gifs/inverted/I-3E.gif)
![I-3F](gifs/inverted/I-3F.gif)
![I-40](gifs/inverted/I-40.gif)
![I-5B](gifs/inverted/I-5B.gif)
![I-5C](gifs/inverted/I-5C.gif)
![I-5D](gifs/inverted/I-5D.gif)
![I-5E](gifs/inverted/I-5E.gif)
![I-60](gifs/inverted/I-60.gif)
![I-7B](gifs/inverted/I-7B.gif)
![I-7C](gifs/inverted/I-7C.gif)
![I-7D](gifs/inverted/I-7D.gif)
![I-7E](gifs/inverted/I-7E.gif)
![I-a](gifs/inverted/I-a.gif)
![I-A](gifs/inverted/I-A.gif)
![I-b](gifs/inverted/I-b.gif)
![I-B](gifs/inverted/I-B.gif)
![I-c](gifs/inverted/I-c.gif)
![I-C](gifs/inverted/I-C.gif)
![I-d](gifs/inverted/I-d.gif)
![I-D](gifs/inverted/I-D.gif)
![I-e](gifs/inverted/I-e.gif)
![I-E](gifs/inverted/I-E.gif)
![I-f](gifs/inverted/I-f.gif)
![I-F](gifs/inverted/I-F.gif)
![I-g](gifs/inverted/I-g.gif)
![I-G](gifs/inverted/I-G.gif)
![I-h](gifs/inverted/I-h.gif)
![I-H](gifs/inverted/I-H.gif)
![I-i](gifs/inverted/I-i.gif)
![I-I](gifs/inverted/I-I.gif)
![I-j](gifs/inverted/I-j.gif)
![I-J](gifs/inverted/I-J.gif)
![I-k](gifs/inverted/I-k.gif)
![I-K](gifs/inverted/I-K.gif)
![I-l](gifs/inverted/I-l.gif)
![I-L](gifs/inverted/I-L.gif)
![I-m](gifs/inverted/I-m.gif)
![I-M](gifs/inverted/I-M.gif)
![I-n](gifs/inverted/I-n.gif)
![I-N](gifs/inverted/I-N.gif)
![I-o](gifs/inverted/I-o.gif)
![I-O](gifs/inverted/I-O.gif)
![I-p](gifs/inverted/I-p.gif)
![I-P](gifs/inverted/I-P.gif)
![I-q](gifs/inverted/I-q.gif)
![I-Q](gifs/inverted/I-Q.gif)
![I-r](gifs/inverted/I-r.gif)
![I-R](gifs/inverted/I-R.gif)
![I-s](gifs/inverted/I-s.gif)
![I-S](gifs/inverted/I-S.gif)
![I-t](gifs/inverted/I-t.gif)
![I-T](gifs/inverted/I-T.gif)
![I-u](gifs/inverted/I-u.gif)
![I-U](gifs/inverted/I-U.gif)
![I-v](gifs/inverted/I-v.gif)
![I-V](gifs/inverted/I-V.gif)
![I-w](gifs/inverted/I-w.gif)
![I-W](gifs/inverted/I-W.gif)
![I-x](gifs/inverted/I-x.gif)
![I-X](gifs/inverted/I-X.gif)
![I-y](gifs/inverted/I-y.gif)
![I-Y](gifs/inverted/I-Y.gif)
![I-z](gifs/inverted/I-z.gif)
![I-Z](gifs/inverted/I-Z.gif)

<br>

## scroll your gifs
using ffmpeg scroll filter, we can scroll our gifs horizontally or vertically

```
for i in *.gif ; do mkdir h-scroll ; ffmpeg -i $i -vf scroll=h=0.09 h-scroll/H-$i ; done
```

![H-0](gifs/h-scroll/H-0.gif)
![H-1](gifs/h-scroll/H-1.gif)
![H-2](gifs/h-scroll/H-2.gif)
![H-3](gifs/h-scroll/H-3.gif)
![H-4](gifs/h-scroll/H-4.gif)
![H-5](gifs/h-scroll/H-5.gif)
![H-6](gifs/h-scroll/H-6.gif)
![H-7](gifs/h-scroll/H-7.gif)
![H-8](gifs/h-scroll/H-8.gif)
![H-9](gifs/h-scroll/H-9.gif)
![H-21](gifs/h-scroll/H-21.gif)
![H-22](gifs/h-scroll/H-22.gif)
![H-23](gifs/h-scroll/H-23.gif)
![H-24](gifs/h-scroll/H-24.gif)
![H-25](gifs/h-scroll/H-25.gif)
![H-26](gifs/h-scroll/H-26.gif)
![H-27](gifs/h-scroll/H-27.gif)
![H-28](gifs/h-scroll/H-28.gif)
![H-29](gifs/h-scroll/H-29.gif)
![H-2A](gifs/h-scroll/H-2A.gif)
![H-2B](gifs/h-scroll/H-2B.gif)
![H-2C](gifs/h-scroll/H-2C.gif)
![H-2D](gifs/h-scroll/H-2D.gif)
![H-2E](gifs/h-scroll/H-2E.gif)
![H-2F](gifs/h-scroll/H-2F.gif)
![H-3A](gifs/h-scroll/H-3A.gif)
![H-3B](gifs/h-scroll/H-3B.gif)
![H-3C](gifs/h-scroll/H-3C.gif)
![H-3D](gifs/h-scroll/H-3D.gif)
![H-3E](gifs/h-scroll/H-3E.gif)
![H-3F](gifs/h-scroll/H-3F.gif)
![H-40](gifs/h-scroll/H-40.gif)
![H-5B](gifs/h-scroll/H-5B.gif)
![H-5C](gifs/h-scroll/H-5C.gif)
![H-5D](gifs/h-scroll/H-5D.gif)
![H-5E](gifs/h-scroll/H-5E.gif)
![H-60](gifs/h-scroll/H-60.gif)
![H-7B](gifs/h-scroll/H-7B.gif)
![H-7C](gifs/h-scroll/H-7C.gif)
![H-7D](gifs/h-scroll/H-7D.gif)
![H-7E](gifs/h-scroll/H-7E.gif)
![H-a](gifs/h-scroll/H-a.gif)
![H-A](gifs/h-scroll/H-A.gif)
![H-b](gifs/h-scroll/H-b.gif)
![H-B](gifs/h-scroll/H-B.gif)
![H-c](gifs/h-scroll/H-c.gif)
![H-C](gifs/h-scroll/H-C.gif)
![H-d](gifs/h-scroll/H-d.gif)
![H-D](gifs/h-scroll/H-D.gif)
![H-e](gifs/h-scroll/H-e.gif)
![H-E](gifs/h-scroll/H-E.gif)
![H-f](gifs/h-scroll/H-f.gif)
![H-F](gifs/h-scroll/H-F.gif)
![H-g](gifs/h-scroll/H-g.gif)
![H-G](gifs/h-scroll/H-G.gif)
![H-h](gifs/h-scroll/H-h.gif)
![H-H](gifs/h-scroll/H-H.gif)
![H-i](gifs/h-scroll/H-i.gif)
![H-I](gifs/h-scroll/H-I.gif)
![H-j](gifs/h-scroll/H-j.gif)
![H-J](gifs/h-scroll/H-J.gif)
![H-k](gifs/h-scroll/H-k.gif)
![H-K](gifs/h-scroll/H-K.gif)
![H-l](gifs/h-scroll/H-l.gif)
![H-L](gifs/h-scroll/H-L.gif)
![H-m](gifs/h-scroll/H-m.gif)
![H-M](gifs/h-scroll/H-M.gif)
![H-n](gifs/h-scroll/H-n.gif)
![H-N](gifs/h-scroll/H-N.gif)
![H-o](gifs/h-scroll/H-o.gif)
![H-O](gifs/h-scroll/H-O.gif)
![H-p](gifs/h-scroll/H-p.gif)
![H-P](gifs/h-scroll/H-P.gif)
![H-q](gifs/h-scroll/H-q.gif)
![H-Q](gifs/h-scroll/H-Q.gif)
![H-r](gifs/h-scroll/H-r.gif)
![H-R](gifs/h-scroll/H-R.gif)
![H-s](gifs/h-scroll/H-s.gif)
![H-S](gifs/h-scroll/H-S.gif)
![H-t](gifs/h-scroll/H-t.gif)
![H-T](gifs/h-scroll/H-T.gif)
![H-u](gifs/h-scroll/H-u.gif)
![H-U](gifs/h-scroll/H-U.gif)
![H-v](gifs/h-scroll/H-v.gif)
![H-V](gifs/h-scroll/H-V.gif)
![H-w](gifs/h-scroll/H-w.gif)
![H-W](gifs/h-scroll/H-W.gif)
![H-x](gifs/h-scroll/H-x.gif)
![H-X](gifs/h-scroll/H-X.gif)
![H-y](gifs/h-scroll/H-y.gif)
![H-Y](gifs/h-scroll/H-Y.gif)
![H-z](gifs/h-scroll/H-z.gif)
![H-Z](gifs/h-scroll/H-Z.gif)

```
for i in *.gif ; do mkdir v-scroll ; ffmpeg -i $i -vf scroll=v=-0.09 v-scroll/V-$i ; done
```

![V-0](gifs/v-scroll/V-0.gif)
![V-1](gifs/v-scroll/V-1.gif)
![V-2](gifs/v-scroll/V-2.gif)
![V-3](gifs/v-scroll/V-3.gif)
![V-4](gifs/v-scroll/V-4.gif)
![V-5](gifs/v-scroll/V-5.gif)
![V-6](gifs/v-scroll/V-6.gif)
![V-7](gifs/v-scroll/V-7.gif)
![V-8](gifs/v-scroll/V-8.gif)
![V-9](gifs/v-scroll/V-9.gif)
![V-21](gifs/v-scroll/V-21.gif)
![V-22](gifs/v-scroll/V-22.gif)
![V-23](gifs/v-scroll/V-23.gif)
![V-24](gifs/v-scroll/V-24.gif)
![V-25](gifs/v-scroll/V-25.gif)
![V-26](gifs/v-scroll/V-26.gif)
![V-27](gifs/v-scroll/V-27.gif)
![V-28](gifs/v-scroll/V-28.gif)
![V-29](gifs/v-scroll/V-29.gif)
![V-2A](gifs/v-scroll/V-2A.gif)
![V-2B](gifs/v-scroll/V-2B.gif)
![V-2C](gifs/v-scroll/V-2C.gif)
![V-2D](gifs/v-scroll/V-2D.gif)
![V-2E](gifs/v-scroll/V-2E.gif)
![V-2F](gifs/v-scroll/V-2F.gif)
![V-3A](gifs/v-scroll/V-3A.gif)
![V-3B](gifs/v-scroll/V-3B.gif)
![V-3C](gifs/v-scroll/V-3C.gif)
![V-3D](gifs/v-scroll/V-3D.gif)
![V-3E](gifs/v-scroll/V-3E.gif)
![V-3F](gifs/v-scroll/V-3F.gif)
![V-40](gifs/v-scroll/V-40.gif)
![V-5B](gifs/v-scroll/V-5B.gif)
![V-5C](gifs/v-scroll/V-5C.gif)
![V-5D](gifs/v-scroll/V-5D.gif)
![V-5E](gifs/v-scroll/V-5E.gif)
![V-60](gifs/v-scroll/V-60.gif)
![V-7B](gifs/v-scroll/V-7B.gif)
![V-7C](gifs/v-scroll/V-7C.gif)
![V-7D](gifs/v-scroll/V-7D.gif)
![V-7E](gifs/v-scroll/V-7E.gif)
![V-a](gifs/v-scroll/V-a.gif)
![V-A](gifs/v-scroll/V-A.gif)
![V-b](gifs/v-scroll/V-b.gif)
![V-B](gifs/v-scroll/V-B.gif)
![V-c](gifs/v-scroll/V-c.gif)
![V-C](gifs/v-scroll/V-C.gif)
![V-d](gifs/v-scroll/V-d.gif)
![V-D](gifs/v-scroll/V-D.gif)
![V-e](gifs/v-scroll/V-e.gif)
![V-E](gifs/v-scroll/V-E.gif)
![V-f](gifs/v-scroll/V-f.gif)
![V-F](gifs/v-scroll/V-F.gif)
![V-g](gifs/v-scroll/V-g.gif)
![V-G](gifs/v-scroll/V-G.gif)
![V-h](gifs/v-scroll/V-h.gif)
![V-H](gifs/v-scroll/V-H.gif)
![V-i](gifs/v-scroll/V-i.gif)
![V-I](gifs/v-scroll/V-I.gif)
![V-j](gifs/v-scroll/V-j.gif)
![V-J](gifs/v-scroll/V-J.gif)
![V-k](gifs/v-scroll/V-k.gif)
![V-K](gifs/v-scroll/V-K.gif)
![V-l](gifs/v-scroll/V-l.gif)
![V-L](gifs/v-scroll/V-L.gif)
![V-m](gifs/v-scroll/V-m.gif)
![V-M](gifs/v-scroll/V-M.gif)
![V-n](gifs/v-scroll/V-n.gif)
![V-N](gifs/v-scroll/V-N.gif)
![V-o](gifs/v-scroll/V-o.gif)
![V-O](gifs/v-scroll/V-O.gif)
![V-p](gifs/v-scroll/V-p.gif)
![V-P](gifs/v-scroll/V-P.gif)
![V-q](gifs/v-scroll/V-q.gif)
![V-Q](gifs/v-scroll/V-Q.gif)
![V-r](gifs/v-scroll/V-r.gif)
![V-R](gifs/v-scroll/V-R.gif)
![V-s](gifs/v-scroll/V-s.gif)
![V-S](gifs/v-scroll/V-S.gif)
![V-t](gifs/v-scroll/V-t.gif)
![V-T](gifs/v-scroll/V-T.gif)
![V-u](gifs/v-scroll/V-u.gif)
![V-U](gifs/v-scroll/V-U.gif)
![V-v](gifs/v-scroll/V-v.gif)
![V-V](gifs/v-scroll/V-V.gif)
![V-w](gifs/v-scroll/V-w.gif)
![V-W](gifs/v-scroll/V-W.gif)
![V-x](gifs/v-scroll/V-x.gif)
![V-X](gifs/v-scroll/V-X.gif)
![V-y](gifs/v-scroll/V-y.gif)
![V-Y](gifs/v-scroll/V-Y.gif)
![V-z](gifs/v-scroll/V-z.gif)
![V-Z](gifs/v-scroll/V-Z.gif)

if you want to reverse the motion either add a negative sign `-` before the values like in our vertical example or do not include it like the horizontal example

<br>

## combine multiple filters
say i don't care about the colors of above animations but i do like motion so let's make it black & white we also use `,` to combine this filter with invert to make a dark variant of those animations

```
for i in *.gif ; do mkdir bw-inv ; ffmpeg -i $i -vf hue=s=0,negate bw-inv/B-$i ; done
```

![B-H-0](gifs/h-bw-inv/B-H-0.gif)
![B-H-1](gifs/h-bw-inv/B-H-1.gif)
![B-H-2](gifs/h-bw-inv/B-H-2.gif)
![B-H-3](gifs/h-bw-inv/B-H-3.gif)
![B-H-4](gifs/h-bw-inv/B-H-4.gif)
![B-H-5](gifs/h-bw-inv/B-H-5.gif)
![B-H-6](gifs/h-bw-inv/B-H-6.gif)
![B-H-7](gifs/h-bw-inv/B-H-7.gif)
![B-H-8](gifs/h-bw-inv/B-H-8.gif)
![B-H-9](gifs/h-bw-inv/B-H-9.gif)
![B-H-21](gifs/h-bw-inv/B-H-21.gif)
![B-H-22](gifs/h-bw-inv/B-H-22.gif)
![B-H-23](gifs/h-bw-inv/B-H-23.gif)
![B-H-24](gifs/h-bw-inv/B-H-24.gif)
![B-H-25](gifs/h-bw-inv/B-H-25.gif)
![B-H-26](gifs/h-bw-inv/B-H-26.gif)
![B-H-27](gifs/h-bw-inv/B-H-27.gif)
![B-H-28](gifs/h-bw-inv/B-H-28.gif)
![B-H-29](gifs/h-bw-inv/B-H-29.gif)
![B-H-2A](gifs/h-bw-inv/B-H-2A.gif)
![B-H-2B](gifs/h-bw-inv/B-H-2B.gif)
![B-H-2C](gifs/h-bw-inv/B-H-2C.gif)
![B-H-2D](gifs/h-bw-inv/B-H-2D.gif)
![B-H-2E](gifs/h-bw-inv/B-H-2E.gif)
![B-H-2F](gifs/h-bw-inv/B-H-2F.gif)
![B-H-3A](gifs/h-bw-inv/B-H-3A.gif)
![B-H-3B](gifs/h-bw-inv/B-H-3B.gif)
![B-H-3C](gifs/h-bw-inv/B-H-3C.gif)
![B-H-3D](gifs/h-bw-inv/B-H-3D.gif)
![B-H-3E](gifs/h-bw-inv/B-H-3E.gif)
![B-H-3F](gifs/h-bw-inv/B-H-3F.gif)
![B-H-40](gifs/h-bw-inv/B-H-40.gif)
![B-H-5B](gifs/h-bw-inv/B-H-5B.gif)
![B-H-5C](gifs/h-bw-inv/B-H-5C.gif)
![B-H-5D](gifs/h-bw-inv/B-H-5D.gif)
![B-H-5E](gifs/h-bw-inv/B-H-5E.gif)
![B-H-60](gifs/h-bw-inv/B-H-60.gif)
![B-H-7B](gifs/h-bw-inv/B-H-7B.gif)
![B-H-7C](gifs/h-bw-inv/B-H-7C.gif)
![B-H-7D](gifs/h-bw-inv/B-H-7D.gif)
![B-H-7E](gifs/h-bw-inv/B-H-7E.gif)
![B-H-a](gifs/h-bw-inv/B-H-a.gif)
![B-H-A](gifs/h-bw-inv/B-H-A.gif)
![B-H-b](gifs/h-bw-inv/B-H-b.gif)
![B-H-B](gifs/h-bw-inv/B-H-B.gif)
![B-H-c](gifs/h-bw-inv/B-H-c.gif)
![B-H-C](gifs/h-bw-inv/B-H-C.gif)
![B-H-d](gifs/h-bw-inv/B-H-d.gif)
![B-H-D](gifs/h-bw-inv/B-H-D.gif)
![B-H-e](gifs/h-bw-inv/B-H-e.gif)
![B-H-E](gifs/h-bw-inv/B-H-E.gif)
![B-H-f](gifs/h-bw-inv/B-H-f.gif)
![B-H-F](gifs/h-bw-inv/B-H-F.gif)
![B-H-g](gifs/h-bw-inv/B-H-g.gif)
![B-H-G](gifs/h-bw-inv/B-H-G.gif)
![B-H-h](gifs/h-bw-inv/B-H-h.gif)
![B-H-H](gifs/h-bw-inv/B-H-H.gif)
![B-H-i](gifs/h-bw-inv/B-H-i.gif)
![B-H-I](gifs/h-bw-inv/B-H-I.gif)
![B-H-j](gifs/h-bw-inv/B-H-j.gif)
![B-H-J](gifs/h-bw-inv/B-H-J.gif)
![B-H-k](gifs/h-bw-inv/B-H-k.gif)
![B-H-K](gifs/h-bw-inv/B-H-K.gif)
![B-H-l](gifs/h-bw-inv/B-H-l.gif)
![B-H-L](gifs/h-bw-inv/B-H-L.gif)
![B-H-m](gifs/h-bw-inv/B-H-m.gif)
![B-H-M](gifs/h-bw-inv/B-H-M.gif)
![B-H-n](gifs/h-bw-inv/B-H-n.gif)
![B-H-N](gifs/h-bw-inv/B-H-N.gif)
![B-H-o](gifs/h-bw-inv/B-H-o.gif)
![B-H-O](gifs/h-bw-inv/B-H-O.gif)
![B-H-p](gifs/h-bw-inv/B-H-p.gif)
![B-H-P](gifs/h-bw-inv/B-H-P.gif)
![B-H-q](gifs/h-bw-inv/B-H-q.gif)
![B-H-Q](gifs/h-bw-inv/B-H-Q.gif)
![B-H-r](gifs/h-bw-inv/B-H-r.gif)
![B-H-R](gifs/h-bw-inv/B-H-R.gif)
![B-H-s](gifs/h-bw-inv/B-H-s.gif)
![B-H-S](gifs/h-bw-inv/B-H-S.gif)
![B-H-t](gifs/h-bw-inv/B-H-t.gif)
![B-H-T](gifs/h-bw-inv/B-H-T.gif)
![B-H-u](gifs/h-bw-inv/B-H-u.gif)
![B-H-U](gifs/h-bw-inv/B-H-U.gif)
![B-H-v](gifs/h-bw-inv/B-H-v.gif)
![B-H-V](gifs/h-bw-inv/B-H-V.gif)
![B-H-w](gifs/h-bw-inv/B-H-w.gif)
![B-H-W](gifs/h-bw-inv/B-H-W.gif)
![B-H-x](gifs/h-bw-inv/B-H-x.gif)
![B-H-X](gifs/h-bw-inv/B-H-X.gif)
![B-H-y](gifs/h-bw-inv/B-H-y.gif)
![B-H-Y](gifs/h-bw-inv/B-H-Y.gif)
![B-H-z](gifs/h-bw-inv/B-H-z.gif)
![B-H-Z](gifs/h-bw-inv/B-H-Z.gif)


![B-V-0](gifs/v-bw-inv/B-V-0.gif)
![B-V-1](gifs/v-bw-inv/B-V-1.gif)
![B-V-2](gifs/v-bw-inv/B-V-2.gif)
![B-V-3](gifs/v-bw-inv/B-V-3.gif)
![B-V-4](gifs/v-bw-inv/B-V-4.gif)
![B-V-5](gifs/v-bw-inv/B-V-5.gif)
![B-V-6](gifs/v-bw-inv/B-V-6.gif)
![B-V-7](gifs/v-bw-inv/B-V-7.gif)
![B-V-8](gifs/v-bw-inv/B-V-8.gif)
![B-V-9](gifs/v-bw-inv/B-V-9.gif)
![B-V-21](gifs/v-bw-inv/B-V-21.gif)
![B-V-22](gifs/v-bw-inv/B-V-22.gif)
![B-V-23](gifs/v-bw-inv/B-V-23.gif)
![B-V-24](gifs/v-bw-inv/B-V-24.gif)
![B-V-25](gifs/v-bw-inv/B-V-25.gif)
![B-V-26](gifs/v-bw-inv/B-V-26.gif)
![B-V-27](gifs/v-bw-inv/B-V-27.gif)
![B-V-28](gifs/v-bw-inv/B-V-28.gif)
![B-V-29](gifs/v-bw-inv/B-V-29.gif)
![B-V-2A](gifs/v-bw-inv/B-V-2A.gif)
![B-V-2B](gifs/v-bw-inv/B-V-2B.gif)
![B-V-2C](gifs/v-bw-inv/B-V-2C.gif)
![B-V-2D](gifs/v-bw-inv/B-V-2D.gif)
![B-V-2E](gifs/v-bw-inv/B-V-2E.gif)
![B-V-2F](gifs/v-bw-inv/B-V-2F.gif)
![B-V-3A](gifs/v-bw-inv/B-V-3A.gif)
![B-V-3B](gifs/v-bw-inv/B-V-3B.gif)
![B-V-3C](gifs/v-bw-inv/B-V-3C.gif)
![B-V-3D](gifs/v-bw-inv/B-V-3D.gif)
![B-V-3E](gifs/v-bw-inv/B-V-3E.gif)
![B-V-3F](gifs/v-bw-inv/B-V-3F.gif)
![B-V-40](gifs/v-bw-inv/B-V-40.gif)
![B-V-5B](gifs/v-bw-inv/B-V-5B.gif)
![B-V-5C](gifs/v-bw-inv/B-V-5C.gif)
![B-V-5D](gifs/v-bw-inv/B-V-5D.gif)
![B-V-5E](gifs/v-bw-inv/B-V-5E.gif)
![B-V-60](gifs/v-bw-inv/B-V-60.gif)
![B-V-7B](gifs/v-bw-inv/B-V-7B.gif)
![B-V-7C](gifs/v-bw-inv/B-V-7C.gif)
![B-V-7D](gifs/v-bw-inv/B-V-7D.gif)
![B-V-7E](gifs/v-bw-inv/B-V-7E.gif)
![B-V-a](gifs/v-bw-inv/B-V-a.gif)
![B-V-A](gifs/v-bw-inv/B-V-A.gif)
![B-V-b](gifs/v-bw-inv/B-V-b.gif)
![B-V-B](gifs/v-bw-inv/B-V-B.gif)
![B-V-c](gifs/v-bw-inv/B-V-c.gif)
![B-V-C](gifs/v-bw-inv/B-V-C.gif)
![B-V-d](gifs/v-bw-inv/B-V-d.gif)
![B-V-D](gifs/v-bw-inv/B-V-D.gif)
![B-V-e](gifs/v-bw-inv/B-V-e.gif)
![B-V-E](gifs/v-bw-inv/B-V-E.gif)
![B-V-f](gifs/v-bw-inv/B-V-f.gif)
![B-V-F](gifs/v-bw-inv/B-V-F.gif)
![B-V-g](gifs/v-bw-inv/B-V-g.gif)
![B-V-G](gifs/v-bw-inv/B-V-G.gif)
![B-V-h](gifs/v-bw-inv/B-V-h.gif)
![B-V-H](gifs/v-bw-inv/B-V-H.gif)
![B-V-i](gifs/v-bw-inv/B-V-i.gif)
![B-V-I](gifs/v-bw-inv/B-V-I.gif)
![B-V-j](gifs/v-bw-inv/B-V-j.gif)
![B-V-J](gifs/v-bw-inv/B-V-J.gif)
![B-V-k](gifs/v-bw-inv/B-V-k.gif)
![B-V-K](gifs/v-bw-inv/B-V-K.gif)
![B-V-l](gifs/v-bw-inv/B-V-l.gif)
![B-V-L](gifs/v-bw-inv/B-V-L.gif)
![B-V-m](gifs/v-bw-inv/B-V-m.gif)
![B-V-M](gifs/v-bw-inv/B-V-M.gif)
![B-V-n](gifs/v-bw-inv/B-V-n.gif)
![B-V-N](gifs/v-bw-inv/B-V-N.gif)
![B-V-o](gifs/v-bw-inv/B-V-o.gif)
![B-V-O](gifs/v-bw-inv/B-V-O.gif)
![B-V-p](gifs/v-bw-inv/B-V-p.gif)
![B-V-P](gifs/v-bw-inv/B-V-P.gif)
![B-V-q](gifs/v-bw-inv/B-V-q.gif)
![B-V-Q](gifs/v-bw-inv/B-V-Q.gif)
![B-V-r](gifs/v-bw-inv/B-V-r.gif)
![B-V-R](gifs/v-bw-inv/B-V-R.gif)
![B-V-s](gifs/v-bw-inv/B-V-s.gif)
![B-V-S](gifs/v-bw-inv/B-V-S.gif)
![B-V-t](gifs/v-bw-inv/B-V-t.gif)
![B-V-T](gifs/v-bw-inv/B-V-T.gif)
![B-V-u](gifs/v-bw-inv/B-V-u.gif)
![B-V-U](gifs/v-bw-inv/B-V-U.gif)
![B-V-v](gifs/v-bw-inv/B-V-v.gif)
![B-V-V](gifs/v-bw-inv/B-V-V.gif)
![B-V-w](gifs/v-bw-inv/B-V-w.gif)
![B-V-W](gifs/v-bw-inv/B-V-W.gif)
![B-V-x](gifs/v-bw-inv/B-V-x.gif)
![B-V-X](gifs/v-bw-inv/B-V-X.gif)
![B-V-y](gifs/v-bw-inv/B-V-y.gif)
![B-V-Y](gifs/v-bw-inv/B-V-Y.gif)
![B-V-z](gifs/v-bw-inv/B-V-z.gif)
![B-V-Z](gifs/v-bw-inv/B-V-Z.gif)

the same results can be achieved with the convert's own `-negate` for the invert and `-monochrome` for black and white filter but since we already had our gifs made i used ffmpeg because it has more options and filters to play with 

<br>

## rotate your characters
convert has a native flag for rotating images and in our case characters so let's use it to create these images and iterate thru them all with rotation

```
for h in {30..360..30} ; for i in {a..z} {A..Z} {0..9} ; do convert -gravity center -trim -background blue -fill cyan -font ./nerd.ttf -size 30x30 caption:$i -rotate $h -extent 30x30 $h-$i.jpg ; done
```

and for special characters

```
for h in {30..360..30} ; for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background blue -fill cyan -rotate $h -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char $h-$hex.jpg ; done
```

for turning everything counter-clock wise just add a negative sign `-` before `$h` like this `-rotate -$h` in both commands to achieve this, lets get to converting these

```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -v *-$m.jpg) RR-$m.gif ; done
```

and for special characters

```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -v *-$m.jpg) RR-$m.gif ; done
```

same two commands can be run on your counter-clock rotation image sequences

![RR-0](gifs/rot-clo/RR-0.gif)
![RR-1](gifs/rot-clo/RR-1.gif)
![RR-2](gifs/rot-clo/RR-2.gif)
![RR-3](gifs/rot-clo/RR-3.gif)
![RR-4](gifs/rot-clo/RR-4.gif)
![RR-5](gifs/rot-clo/RR-5.gif)
![RR-6](gifs/rot-clo/RR-6.gif)
![RR-7](gifs/rot-clo/RR-7.gif)
![RR-8](gifs/rot-clo/RR-8.gif)
![RR-9](gifs/rot-clo/RR-9.gif)
![RR-21](gifs/rot-clo/RR-21.gif)
![RR-22](gifs/rot-clo/RR-22.gif)
![RR-23](gifs/rot-clo/RR-23.gif)
![RR-24](gifs/rot-clo/RR-24.gif)
![RR-25](gifs/rot-clo/RR-25.gif)
![RR-26](gifs/rot-clo/RR-26.gif)
![RR-27](gifs/rot-clo/RR-27.gif)
![RR-28](gifs/rot-clo/RR-28.gif)
![RR-29](gifs/rot-clo/RR-29.gif)
![RR-2A](gifs/rot-clo/RR-2A.gif)
![RR-2B](gifs/rot-clo/RR-2B.gif)
![RR-2C](gifs/rot-clo/RR-2C.gif)
![RR-2D](gifs/rot-clo/RR-2D.gif)
![RR-2E](gifs/rot-clo/RR-2E.gif)
![RR-2F](gifs/rot-clo/RR-2F.gif)
![RR-3A](gifs/rot-clo/RR-3A.gif)
![RR-3B](gifs/rot-clo/RR-3B.gif)
![RR-3C](gifs/rot-clo/RR-3C.gif)
![RR-3D](gifs/rot-clo/RR-3D.gif)
![RR-3E](gifs/rot-clo/RR-3E.gif)
![RR-3F](gifs/rot-clo/RR-3F.gif)
![RR-40](gifs/rot-clo/RR-40.gif)
![RR-5B](gifs/rot-clo/RR-5B.gif)
![RR-5C](gifs/rot-clo/RR-5C.gif)
![RR-5D](gifs/rot-clo/RR-5D.gif)
![RR-5E](gifs/rot-clo/RR-5E.gif)
![RR-60](gifs/rot-clo/RR-60.gif)
![RR-7B](gifs/rot-clo/RR-7B.gif)
![RR-7C](gifs/rot-clo/RR-7C.gif)
![RR-7D](gifs/rot-clo/RR-7D.gif)
![RR-7E](gifs/rot-clo/RR-7E.gif)
![RR-a](gifs/rot-clo/RR-a.gif)
![RR-A](gifs/rot-clo/RR-A.gif)
![RR-b](gifs/rot-clo/RR-b.gif)
![RR-B](gifs/rot-clo/RR-B.gif)
![RR-c](gifs/rot-clo/RR-c.gif)
![RR-C](gifs/rot-clo/RR-C.gif)
![RR-d](gifs/rot-clo/RR-d.gif)
![RR-D](gifs/rot-clo/RR-D.gif)
![RR-e](gifs/rot-clo/RR-e.gif)
![RR-E](gifs/rot-clo/RR-E.gif)
![RR-f](gifs/rot-clo/RR-f.gif)
![RR-F](gifs/rot-clo/RR-F.gif)
![RR-g](gifs/rot-clo/RR-g.gif)
![RR-G](gifs/rot-clo/RR-G.gif)
![RR-h](gifs/rot-clo/RR-h.gif)
![RR-H](gifs/rot-clo/RR-H.gif)
![RR-i](gifs/rot-clo/RR-i.gif)
![RR-I](gifs/rot-clo/RR-I.gif)
![RR-j](gifs/rot-clo/RR-j.gif)
![RR-J](gifs/rot-clo/RR-J.gif)
![RR-k](gifs/rot-clo/RR-k.gif)
![RR-K](gifs/rot-clo/RR-K.gif)
![RR-l](gifs/rot-clo/RR-l.gif)
![RR-L](gifs/rot-clo/RR-L.gif)
![RR-m](gifs/rot-clo/RR-m.gif)
![RR-M](gifs/rot-clo/RR-M.gif)
![RR-n](gifs/rot-clo/RR-n.gif)
![RR-N](gifs/rot-clo/RR-N.gif)
![RR-o](gifs/rot-clo/RR-o.gif)
![RR-O](gifs/rot-clo/RR-O.gif)
![RR-p](gifs/rot-clo/RR-p.gif)
![RR-P](gifs/rot-clo/RR-P.gif)
![RR-q](gifs/rot-clo/RR-q.gif)
![RR-Q](gifs/rot-clo/RR-Q.gif)
![RR-r](gifs/rot-clo/RR-r.gif)
![RR-R](gifs/rot-clo/RR-R.gif)
![RR-s](gifs/rot-clo/RR-s.gif)
![RR-S](gifs/rot-clo/RR-S.gif)
![RR-t](gifs/rot-clo/RR-t.gif)
![RR-T](gifs/rot-clo/RR-T.gif)
![RR-u](gifs/rot-clo/RR-u.gif)
![RR-U](gifs/rot-clo/RR-U.gif)
![RR-v](gifs/rot-clo/RR-v.gif)
![RR-V](gifs/rot-clo/RR-V.gif)
![RR-w](gifs/rot-clo/RR-w.gif)
![RR-W](gifs/rot-clo/RR-W.gif)
![RR-x](gifs/rot-clo/RR-x.gif)
![RR-X](gifs/rot-clo/RR-X.gif)
![RR-y](gifs/rot-clo/RR-y.gif)
![RR-Y](gifs/rot-clo/RR-Y.gif)
![RR-z](gifs/rot-clo/RR-z.gif)
![RR-Z](gifs/rot-clo/RR-Z.gif)


![RL-0](gifs/rot-cclo/RL-0.gif)
![RL-1](gifs/rot-cclo/RL-1.gif)
![RL-2](gifs/rot-cclo/RL-2.gif)
![RL-3](gifs/rot-cclo/RL-3.gif)
![RL-4](gifs/rot-cclo/RL-4.gif)
![RL-5](gifs/rot-cclo/RL-5.gif)
![RL-6](gifs/rot-cclo/RL-6.gif)
![RL-7](gifs/rot-cclo/RL-7.gif)
![RL-8](gifs/rot-cclo/RL-8.gif)
![RL-9](gifs/rot-cclo/RL-9.gif)
![RL-21](gifs/rot-cclo/RL-21.gif)
![RL-22](gifs/rot-cclo/RL-22.gif)
![RL-23](gifs/rot-cclo/RL-23.gif)
![RL-24](gifs/rot-cclo/RL-24.gif)
![RL-25](gifs/rot-cclo/RL-25.gif)
![RL-26](gifs/rot-cclo/RL-26.gif)
![RL-27](gifs/rot-cclo/RL-27.gif)
![RL-28](gifs/rot-cclo/RL-28.gif)
![RL-29](gifs/rot-cclo/RL-29.gif)
![RL-2A](gifs/rot-cclo/RL-2A.gif)
![RL-2B](gifs/rot-cclo/RL-2B.gif)
![RL-2C](gifs/rot-cclo/RL-2C.gif)
![RL-2D](gifs/rot-cclo/RL-2D.gif)
![RL-2E](gifs/rot-cclo/RL-2E.gif)
![RL-2F](gifs/rot-cclo/RL-2F.gif)
![RL-3A](gifs/rot-cclo/RL-3A.gif)
![RL-3B](gifs/rot-cclo/RL-3B.gif)
![RL-3C](gifs/rot-cclo/RL-3C.gif)
![RL-3D](gifs/rot-cclo/RL-3D.gif)
![RL-3E](gifs/rot-cclo/RL-3E.gif)
![RL-3F](gifs/rot-cclo/RL-3F.gif)
![RL-40](gifs/rot-cclo/RL-40.gif)
![RL-5B](gifs/rot-cclo/RL-5B.gif)
![RL-5C](gifs/rot-cclo/RL-5C.gif)
![RL-5D](gifs/rot-cclo/RL-5D.gif)
![RL-5E](gifs/rot-cclo/RL-5E.gif)
![RL-60](gifs/rot-cclo/RL-60.gif)
![RL-7B](gifs/rot-cclo/RL-7B.gif)
![RL-7C](gifs/rot-cclo/RL-7C.gif)
![RL-7D](gifs/rot-cclo/RL-7D.gif)
![RL-7E](gifs/rot-cclo/RL-7E.gif)
![RL-a](gifs/rot-cclo/RL-a.gif)
![RL-A](gifs/rot-cclo/RL-A.gif)
![RL-b](gifs/rot-cclo/RL-b.gif)
![RL-B](gifs/rot-cclo/RL-B.gif)
![RL-c](gifs/rot-cclo/RL-c.gif)
![RL-C](gifs/rot-cclo/RL-C.gif)
![RL-d](gifs/rot-cclo/RL-d.gif)
![RL-D](gifs/rot-cclo/RL-D.gif)
![RL-e](gifs/rot-cclo/RL-e.gif)
![RL-E](gifs/rot-cclo/RL-E.gif)
![RL-f](gifs/rot-cclo/RL-f.gif)
![RL-F](gifs/rot-cclo/RL-F.gif)
![RL-g](gifs/rot-cclo/RL-g.gif)
![RL-G](gifs/rot-cclo/RL-G.gif)
![RL-h](gifs/rot-cclo/RL-h.gif)
![RL-H](gifs/rot-cclo/RL-H.gif)
![RL-i](gifs/rot-cclo/RL-i.gif)
![RL-I](gifs/rot-cclo/RL-I.gif)
![RL-j](gifs/rot-cclo/RL-j.gif)
![RL-J](gifs/rot-cclo/RL-J.gif)
![RL-k](gifs/rot-cclo/RL-k.gif)
![RL-K](gifs/rot-cclo/RL-K.gif)
![RL-l](gifs/rot-cclo/RL-l.gif)
![RL-L](gifs/rot-cclo/RL-L.gif)
![RL-m](gifs/rot-cclo/RL-m.gif)
![RL-M](gifs/rot-cclo/RL-M.gif)
![RL-n](gifs/rot-cclo/RL-n.gif)
![RL-N](gifs/rot-cclo/RL-N.gif)
![RL-o](gifs/rot-cclo/RL-o.gif)
![RL-O](gifs/rot-cclo/RL-O.gif)
![RL-p](gifs/rot-cclo/RL-p.gif)
![RL-P](gifs/rot-cclo/RL-P.gif)
![RL-q](gifs/rot-cclo/RL-q.gif)
![RL-Q](gifs/rot-cclo/RL-Q.gif)
![RL-r](gifs/rot-cclo/RL-r.gif)
![RL-R](gifs/rot-cclo/RL-R.gif)
![RL-s](gifs/rot-cclo/RL-s.gif)
![RL-S](gifs/rot-cclo/RL-S.gif)
![RL-t](gifs/rot-cclo/RL-t.gif)
![RL-T](gifs/rot-cclo/RL-T.gif)
![RL-u](gifs/rot-cclo/RL-u.gif)
![RL-U](gifs/rot-cclo/RL-U.gif)
![RL-v](gifs/rot-cclo/RL-v.gif)
![RL-V](gifs/rot-cclo/RL-V.gif)
![RL-w](gifs/rot-cclo/RL-w.gif)
![RL-W](gifs/rot-cclo/RL-W.gif)
![RL-x](gifs/rot-cclo/RL-x.gif)
![RL-X](gifs/rot-cclo/RL-X.gif)
![RL-y](gifs/rot-cclo/RL-y.gif)
![RL-Y](gifs/rot-cclo/RL-Y.gif)
![RL-z](gifs/rot-cclo/RL-z.gif)
![RL-Z](gifs/rot-cclo/RL-Z.gif)

<br>

## using shades of grey as color
imagemagick uses a wide variety of color values and names as input, look [here](https://imagemagick.org/script/color.php) for a complete explanation, but the easiest way to use this is by choosing color names, for the shades of grey specifically there are grey0 which is a black color to grey100 which is a white color and everything between grey1 and grey99 are shades of grey, knowing this we can easily loop thru them in a for loop like this 
```
for i in {0..9} {a..z} {A..Z} ; for g in {0..100..10} ; do convert -gravity center -trim -background grey50 -fill grey$g -font ./nerd.ttf -size 30x30 caption:$i -extent 30x30 $g-$i.jpg ; done
```
as you can see we just need to loop thru the numbers and append them to the grey word in the -fill flag `-fill grey$g` we also only use every 10th number in the loop for a total of 10 frames, the background color stays the same as a neutral grey50, now for converting
```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -v *-$m.jpg) $m.gif ; done
```
for special characters do 
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for g in {0..100..10} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background grey50 -fill grey$g -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char $g-$hex.jpg ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -v *-$m.jpg) g-$m.gif ; done
```

![g-0](gifs/grey/g-0.gif)
![g-1](gifs/grey/g-1.gif)
![g-2](gifs/grey/g-2.gif)
![g-3](gifs/grey/g-3.gif)
![g-4](gifs/grey/g-4.gif)
![g-5](gifs/grey/g-5.gif)
![g-6](gifs/grey/g-6.gif)
![g-7](gifs/grey/g-7.gif)
![g-8](gifs/grey/g-8.gif)
![g-9](gifs/grey/g-9.gif)
![g-21](gifs/grey/g-21.gif)
![g-22](gifs/grey/g-22.gif)
![g-23](gifs/grey/g-23.gif)
![g-24](gifs/grey/g-24.gif)
![g-25](gifs/grey/g-25.gif)
![g-26](gifs/grey/g-26.gif)
![g-27](gifs/grey/g-27.gif)
![g-28](gifs/grey/g-28.gif)
![g-29](gifs/grey/g-29.gif)
![g-2A](gifs/grey/g-2A.gif)
![g-2B](gifs/grey/g-2B.gif)
![g-2C](gifs/grey/g-2C.gif)
![g-2D](gifs/grey/g-2D.gif)
![g-2E](gifs/grey/g-2E.gif)
![g-2F](gifs/grey/g-2F.gif)
![g-3A](gifs/grey/g-3A.gif)
![g-3B](gifs/grey/g-3B.gif)
![g-3C](gifs/grey/g-3C.gif)
![g-3D](gifs/grey/g-3D.gif)
![g-3E](gifs/grey/g-3E.gif)
![g-3F](gifs/grey/g-3F.gif)
![g-40](gifs/grey/g-40.gif)
![g-5B](gifs/grey/g-5B.gif)
![g-5C](gifs/grey/g-5C.gif)
![g-5D](gifs/grey/g-5D.gif)
![g-5E](gifs/grey/g-5E.gif)
![g-60](gifs/grey/g-60.gif)
![g-7B](gifs/grey/g-7B.gif)
![g-7C](gifs/grey/g-7C.gif)
![g-7D](gifs/grey/g-7D.gif)
![g-7E](gifs/grey/g-7E.gif)
![g-a](gifs/grey/g-a.gif)
![g-A](gifs/grey/g-A.gif)
![g-b](gifs/grey/g-b.gif)
![g-B](gifs/grey/g-B.gif)
![g-c](gifs/grey/g-c.gif)
![g-C](gifs/grey/g-C.gif)
![g-d](gifs/grey/g-d.gif)
![g-D](gifs/grey/g-D.gif)
![g-e](gifs/grey/g-e.gif)
![g-E](gifs/grey/g-E.gif)
![g-f](gifs/grey/g-f.gif)
![g-F](gifs/grey/g-F.gif)
![g-g](gifs/grey/g-g.gif)
![g-G](gifs/grey/g-G.gif)
![g-h](gifs/grey/g-h.gif)
![g-H](gifs/grey/g-H.gif)
![g-i](gifs/grey/g-i.gif)
![g-I](gifs/grey/g-I.gif)
![g-j](gifs/grey/g-j.gif)
![g-J](gifs/grey/g-J.gif)
![g-k](gifs/grey/g-k.gif)
![g-K](gifs/grey/g-K.gif)
![g-l](gifs/grey/g-l.gif)
![g-L](gifs/grey/g-L.gif)
![g-m](gifs/grey/g-m.gif)
![g-M](gifs/grey/g-M.gif)
![g-n](gifs/grey/g-n.gif)
![g-N](gifs/grey/g-N.gif)
![g-o](gifs/grey/g-o.gif)
![g-O](gifs/grey/g-O.gif)
![g-p](gifs/grey/g-p.gif)
![g-P](gifs/grey/g-P.gif)
![g-q](gifs/grey/g-q.gif)
![g-Q](gifs/grey/g-Q.gif)
![g-r](gifs/grey/g-r.gif)
![g-R](gifs/grey/g-R.gif)
![g-s](gifs/grey/g-s.gif)
![g-S](gifs/grey/g-S.gif)
![g-t](gifs/grey/g-t.gif)
![g-T](gifs/grey/g-T.gif)
![g-u](gifs/grey/g-u.gif)
![g-U](gifs/grey/g-U.gif)
![g-v](gifs/grey/g-v.gif)
![g-V](gifs/grey/g-V.gif)
![g-w](gifs/grey/g-w.gif)
![g-W](gifs/grey/g-W.gif)
![g-x](gifs/grey/g-x.gif)
![g-X](gifs/grey/g-X.gif)
![g-y](gifs/grey/g-y.gif)
![g-Y](gifs/grey/g-Y.gif)
![g-z](gifs/grey/g-z.gif)
![g-Z](gifs/grey/g-Z.gif)

<br>

## merge multiple files together
using `-adjoin` we can easily combine multiple images to make a gif file
```
convert -adjoin $(ls -v *.jpg) all.gif
```
![all](temp/all.gif)

if you want to change the framerate of these gifs we can use the `-delay` flag, by default convert has a 100 ticks (same as milliseconds) per seconds, any amount of delay we add gets divided by this number and applied before each image in our sequence of images, so the number 8 results in 12.5 frames per second, 16 results in 6.25 fps and so on
```
convert -adjoin -delay 16 $(ls -v *.jpg) all+.gif
```
![all+](temp/all+.gif)

combining multiple gifs together can be done using the same joining method
```
convert -adjoin $(ls -v *.gif) numbers.gif
```
![numbers](temp/numbers.gif)

<br>

## making a smooth gradient animation, the hard way
in one of the above sections i showed how to use ffmpeg's hue filter to make a gradient with colors, it gets the job done but sometimes you want more control with exact colors you want to use

imagemagick gives many options for specifying colors, in our case we'll use `rgb(100%, 0%, 0%)` which takes percentages as RGB values, lets start by changing the colors from red `rgb(100%, 0%, 0%)` to magenta `rgb(100%, 0%, 100%)` with 10% increments
```
for i in {a..z} {A..Z} {0..9} ; for g in {0..100..10} ; do convert -gravity center -trim -background "rgb(100%,0%,$g%)" -fill white -font ./nerd.ttf -size 30x30 caption:$i -extent 30x30 A-$g-$i.jpg ; done
```
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for g in {0..100..10} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background "rgb(100%,0%,$g%)" -fill white -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char A-$g-$hex.jpg ; done
```

<br>

now, make a loop that changes magenta `rgb(100%, 0%, 100%)` to blue `rgb(0%, 0%, 100%)`
```
for i in {a..z} {A..Z} {0..9} ; for g in {100..0..10} ; do convert -gravity center -trim -background "rgb($g%,0%,100%)" -fill white -font ./nerd.ttf -size 30x30 caption:$i -extent 30x30 B-$g-$i.jpg ; done
```
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for g in {0..100..10} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background "rgb($g%,0%,100%)" -fill white -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char B-$g-$hex.jpg ; done
```

<br>

now convert your first batch of images to gifs
```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -v A-*-$m.jpg) A1-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -v A-*-$m.jpg) A1-$m.gif ; done   
```

![A1-0](gifs/gradient/01/A1-0.gif)
![A1-1](gifs/gradient/01/A1-1.gif)
![A1-2](gifs/gradient/01/A1-2.gif)
![A1-3](gifs/gradient/01/A1-3.gif)
![A1-4](gifs/gradient/01/A1-4.gif)
![A1-5](gifs/gradient/01/A1-5.gif)
![A1-6](gifs/gradient/01/A1-6.gif)
![A1-7](gifs/gradient/01/A1-7.gif)
![A1-8](gifs/gradient/01/A1-8.gif)
![A1-9](gifs/gradient/01/A1-9.gif)

<br>

convert the second batch of images to gifs
```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -vr B-*-$m.jpg) A2-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -vr B-*-$m.jpg) A2-$m.gif ; done  
```

note that we use the `-r` flag with ls to sort and feed images in reverse for the second batch of gifs

![A2-0](gifs/gradient/02/A2-0.gif)
![A2-1](gifs/gradient/02/A2-1.gif)
![A2-2](gifs/gradient/02/A2-2.gif)
![A2-3](gifs/gradient/02/A2-3.gif)
![A2-4](gifs/gradient/02/A2-4.gif)
![A2-5](gifs/gradient/02/A2-5.gif)
![A2-6](gifs/gradient/02/A2-6.gif)
![A2-7](gifs/gradient/02/A2-7.gif)
![A2-8](gifs/gradient/02/A2-8.gif)
![A2-9](gifs/gradient/02/A2-9.gif)

<br>

combine both sets of gifs together
```
for m in {a..z} {A..Z} {0..9} ; do convert -adjoin A1-$m.gif A2-$m.gif A3-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -adjoin A1-$m.gif A2-$m.gif A3-$m.gif ; done
```

![A3-0](gifs/gradient/03/A3-0.gif)
![A3-1](gifs/gradient/03/A3-1.gif)
![A3-2](gifs/gradient/03/A3-2.gif)
![A3-3](gifs/gradient/03/A3-3.gif)
![A3-4](gifs/gradient/03/A3-4.gif)
![A3-5](gifs/gradient/03/A3-5.gif)
![A3-6](gifs/gradient/03/A3-6.gif)
![A3-7](gifs/gradient/03/A3-7.gif)
![A3-8](gifs/gradient/03/A3-8.gif)
![A3-9](gifs/gradient/03/A3-9.gif)

<br>

now make a reversed duplicated sets of these gifs to have a smooth back and forth motion in the last step
```
for m in {a..z} {A..Z} {0..9} ; do convert -reverse A3-$m.gif A4-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -reverse A3-$m.gif A4-$m.gif ; done
```

![A4-0](gifs/gradient/04/A4-0.gif)
![A4-1](gifs/gradient/04/A4-1.gif)
![A4-2](gifs/gradient/04/A4-2.gif)
![A4-3](gifs/gradient/04/A4-3.gif)
![A4-4](gifs/gradient/04/A4-4.gif)
![A4-5](gifs/gradient/04/A4-5.gif)
![A4-6](gifs/gradient/04/A4-6.gif)
![A4-7](gifs/gradient/04/A4-7.gif)
![A4-8](gifs/gradient/04/A4-8.gif)
![A4-9](gifs/gradient/04/A4-9.gif)

<br>

finally combine your 3rd and 4th batches of gifs to get the final result
```
for m in {a..z} {A..Z} {0..9} ; do convert -adjoin A3-$m.gif A4-$m.gif A5-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -adjoin A3-$m.gif A4-$m.gif A5-$m.gif ; done
```

![A5-0](gifs/gradient/A5-0.gif)
![A5-1](gifs/gradient/A5-1.gif)
![A5-2](gifs/gradient/A5-2.gif)
![A5-3](gifs/gradient/A5-3.gif)
![A5-4](gifs/gradient/A5-4.gif)
![A5-5](gifs/gradient/A5-5.gif)
![A5-6](gifs/gradient/A5-6.gif)
![A5-7](gifs/gradient/A5-7.gif)
![A5-8](gifs/gradient/A5-8.gif)
![A5-9](gifs/gradient/A5-9.gif)
![A5-21](gifs/gradient/A5-21.gif)
![A5-22](gifs/gradient/A5-22.gif)
![A5-23](gifs/gradient/A5-23.gif)
![A5-24](gifs/gradient/A5-24.gif)
![A5-25](gifs/gradient/A5-25.gif)
![A5-26](gifs/gradient/A5-26.gif)
![A5-27](gifs/gradient/A5-27.gif)
![A5-28](gifs/gradient/A5-28.gif)
![A5-29](gifs/gradient/A5-29.gif)
![A5-2A](gifs/gradient/A5-2A.gif)
![A5-2B](gifs/gradient/A5-2B.gif)
![A5-2C](gifs/gradient/A5-2C.gif)
![A5-2D](gifs/gradient/A5-2D.gif)
![A5-2E](gifs/gradient/A5-2E.gif)
![A5-2F](gifs/gradient/A5-2F.gif)
![A5-3A](gifs/gradient/A5-3A.gif)
![A5-3B](gifs/gradient/A5-3B.gif)
![A5-3C](gifs/gradient/A5-3C.gif)
![A5-3D](gifs/gradient/A5-3D.gif)
![A5-3E](gifs/gradient/A5-3E.gif)
![A5-3F](gifs/gradient/A5-3F.gif)
![A5-40](gifs/gradient/A5-40.gif)
![A5-5B](gifs/gradient/A5-5B.gif)
![A5-5C](gifs/gradient/A5-5C.gif)
![A5-5D](gifs/gradient/A5-5D.gif)
![A5-5E](gifs/gradient/A5-5E.gif)
![A5-60](gifs/gradient/A5-60.gif)
![A5-7B](gifs/gradient/A5-7B.gif)
![A5-7C](gifs/gradient/A5-7C.gif)
![A5-7D](gifs/gradient/A5-7D.gif)
![A5-7E](gifs/gradient/A5-7E.gif)
![A5-a](gifs/gradient/A5-a.gif)
![A5-A](gifs/gradient/A5-A.gif)
![A5-b](gifs/gradient/A5-b.gif)
![A5-B](gifs/gradient/A5-B.gif)
![A5-c](gifs/gradient/A5-c.gif)
![A5-C](gifs/gradient/A5-C.gif)
![A5-d](gifs/gradient/A5-d.gif)
![A5-D](gifs/gradient/A5-D.gif)
![A5-e](gifs/gradient/A5-e.gif)
![A5-E](gifs/gradient/A5-E.gif)
![A5-f](gifs/gradient/A5-f.gif)
![A5-F](gifs/gradient/A5-F.gif)
![A5-g](gifs/gradient/A5-g.gif)
![A5-G](gifs/gradient/A5-G.gif)
![A5-h](gifs/gradient/A5-h.gif)
![A5-H](gifs/gradient/A5-H.gif)
![A5-i](gifs/gradient/A5-i.gif)
![A5-I](gifs/gradient/A5-I.gif)
![A5-j](gifs/gradient/A5-j.gif)
![A5-J](gifs/gradient/A5-J.gif)
![A5-k](gifs/gradient/A5-k.gif)
![A5-K](gifs/gradient/A5-K.gif)
![A5-l](gifs/gradient/A5-l.gif)
![A5-L](gifs/gradient/A5-L.gif)
![A5-m](gifs/gradient/A5-m.gif)
![A5-M](gifs/gradient/A5-M.gif)
![A5-n](gifs/gradient/A5-n.gif)
![A5-N](gifs/gradient/A5-N.gif)
![A5-o](gifs/gradient/A5-o.gif)
![A5-O](gifs/gradient/A5-O.gif)
![A5-p](gifs/gradient/A5-p.gif)
![A5-P](gifs/gradient/A5-P.gif)
![A5-q](gifs/gradient/A5-q.gif)
![A5-Q](gifs/gradient/A5-Q.gif)
![A5-r](gifs/gradient/A5-r.gif)
![A5-R](gifs/gradient/A5-R.gif)
![A5-s](gifs/gradient/A5-s.gif)
![A5-S](gifs/gradient/A5-S.gif)
![A5-t](gifs/gradient/A5-t.gif)
![A5-T](gifs/gradient/A5-T.gif)
![A5-u](gifs/gradient/A5-u.gif)
![A5-U](gifs/gradient/A5-U.gif)
![A5-v](gifs/gradient/A5-v.gif)
![A5-V](gifs/gradient/A5-V.gif)
![A5-w](gifs/gradient/A5-w.gif)
![A5-W](gifs/gradient/A5-W.gif)
![A5-x](gifs/gradient/A5-x.gif)
![A5-X](gifs/gradient/A5-X.gif)
![A5-y](gifs/gradient/A5-y.gif)
![A5-Y](gifs/gradient/A5-Y.gif)
![A5-z](gifs/gradient/A5-z.gif)
![A5-Z](gifs/gradient/A5-Z.gif)

<br>

for the bonus round, lets invert these gifs using convert's own `-negate` and make it like these are completely new gifs
```
for m in {a..z} {A..Z} {0..9} ; do convert -negate A5-$m.gif A6-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -negate A5-$m.gif A6-$m.gif ; done
```

![A6-0](gifs/gradient/A6-0.gif)
![A6-1](gifs/gradient/A6-1.gif)
![A6-2](gifs/gradient/A6-2.gif)
![A6-3](gifs/gradient/A6-3.gif)
![A6-4](gifs/gradient/A6-4.gif)
![A6-5](gifs/gradient/A6-5.gif)
![A6-6](gifs/gradient/A6-6.gif)
![A6-7](gifs/gradient/A6-7.gif)
![A6-8](gifs/gradient/A6-8.gif)
![A6-9](gifs/gradient/A6-9.gif)
![A6-21](gifs/gradient/A6-21.gif)
![A6-22](gifs/gradient/A6-22.gif)
![A6-23](gifs/gradient/A6-23.gif)
![A6-24](gifs/gradient/A6-24.gif)
![A6-25](gifs/gradient/A6-25.gif)
![A6-26](gifs/gradient/A6-26.gif)
![A6-27](gifs/gradient/A6-27.gif)
![A6-28](gifs/gradient/A6-28.gif)
![A6-29](gifs/gradient/A6-29.gif)
![A6-2A](gifs/gradient/A6-2A.gif)
![A6-2B](gifs/gradient/A6-2B.gif)
![A6-2C](gifs/gradient/A6-2C.gif)
![A6-2D](gifs/gradient/A6-2D.gif)
![A6-2E](gifs/gradient/A6-2E.gif)
![A6-2F](gifs/gradient/A6-2F.gif)
![A6-3A](gifs/gradient/A6-3A.gif)
![A6-3B](gifs/gradient/A6-3B.gif)
![A6-3C](gifs/gradient/A6-3C.gif)
![A6-3D](gifs/gradient/A6-3D.gif)
![A6-3E](gifs/gradient/A6-3E.gif)
![A6-3F](gifs/gradient/A6-3F.gif)
![A6-40](gifs/gradient/A6-40.gif)
![A6-5B](gifs/gradient/A6-5B.gif)
![A6-5C](gifs/gradient/A6-5C.gif)
![A6-5D](gifs/gradient/A6-5D.gif)
![A6-5E](gifs/gradient/A6-5E.gif)
![A6-60](gifs/gradient/A6-60.gif)
![A6-7B](gifs/gradient/A6-7B.gif)
![A6-7C](gifs/gradient/A6-7C.gif)
![A6-7D](gifs/gradient/A6-7D.gif)
![A6-7E](gifs/gradient/A6-7E.gif)
![A6-a](gifs/gradient/A6-a.gif)
![A6-A](gifs/gradient/A6-A.gif)
![A6-b](gifs/gradient/A6-b.gif)
![A6-B](gifs/gradient/A6-B.gif)
![A6-c](gifs/gradient/A6-c.gif)
![A6-C](gifs/gradient/A6-C.gif)
![A6-d](gifs/gradient/A6-d.gif)
![A6-D](gifs/gradient/A6-D.gif)
![A6-e](gifs/gradient/A6-e.gif)
![A6-E](gifs/gradient/A6-E.gif)
![A6-f](gifs/gradient/A6-f.gif)
![A6-F](gifs/gradient/A6-F.gif)
![A6-g](gifs/gradient/A6-g.gif)
![A6-G](gifs/gradient/A6-G.gif)
![A6-h](gifs/gradient/A6-h.gif)
![A6-H](gifs/gradient/A6-H.gif)
![A6-i](gifs/gradient/A6-i.gif)
![A6-I](gifs/gradient/A6-I.gif)
![A6-j](gifs/gradient/A6-j.gif)
![A6-J](gifs/gradient/A6-J.gif)
![A6-k](gifs/gradient/A6-k.gif)
![A6-K](gifs/gradient/A6-K.gif)
![A6-l](gifs/gradient/A6-l.gif)
![A6-L](gifs/gradient/A6-L.gif)
![A6-m](gifs/gradient/A6-m.gif)
![A6-M](gifs/gradient/A6-M.gif)
![A6-n](gifs/gradient/A6-n.gif)
![A6-N](gifs/gradient/A6-N.gif)
![A6-o](gifs/gradient/A6-o.gif)
![A6-O](gifs/gradient/A6-O.gif)
![A6-p](gifs/gradient/A6-p.gif)
![A6-P](gifs/gradient/A6-P.gif)
![A6-q](gifs/gradient/A6-q.gif)
![A6-Q](gifs/gradient/A6-Q.gif)
![A6-r](gifs/gradient/A6-r.gif)
![A6-R](gifs/gradient/A6-R.gif)
![A6-s](gifs/gradient/A6-s.gif)
![A6-S](gifs/gradient/A6-S.gif)
![A6-t](gifs/gradient/A6-t.gif)
![A6-T](gifs/gradient/A6-T.gif)
![A6-u](gifs/gradient/A6-u.gif)
![A6-U](gifs/gradient/A6-U.gif)
![A6-v](gifs/gradient/A6-v.gif)
![A6-V](gifs/gradient/A6-V.gif)
![A6-w](gifs/gradient/A6-w.gif)
![A6-W](gifs/gradient/A6-W.gif)
![A6-x](gifs/gradient/A6-x.gif)
![A6-X](gifs/gradient/A6-X.gif)
![A6-y](gifs/gradient/A6-y.gif)
![A6-Y](gifs/gradient/A6-Y.gif)
![A6-z](gifs/gradient/A6-z.gif)
![A6-Z](gifs/gradient/A6-Z.gif)

<br>

## variable sizes
using `-pointsize` flag we can set the size of our characters in our for loop
```
for i in {a..z} {A..Z} {0..9} ; for s in {5..50..5} ; do convert -gravity center -trim -background grey25 -fill grey75 -font ./nerd.ttf -size 30x30 -pointsize $s caption:$i -extent 30x30 $i-$s.jpg ; done
```
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for s in {5..50..5} ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background grey25 -fill grey75 -font ./nerd.ttf -size 30x30 -extent 30x30 -pointsize $s caption:$char $hex-$s.jpg ; done
```
now for converting them
```
for m in {a..z} {A..Z} {0..9} ; do convert -delay 8 $(ls -v $m-*.jpg) S-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -delay 8 $(ls -v $m-*.jpg) S-$m.gif ; done 
```

![S-0](gifs/size/S-0.gif)
![S-1](gifs/size/S-1.gif)
![S-2](gifs/size/S-2.gif)
![S-3](gifs/size/S-3.gif)
![S-4](gifs/size/S-4.gif)
![S-5](gifs/size/S-5.gif)
![S-6](gifs/size/S-6.gif)
![S-7](gifs/size/S-7.gif)
![S-8](gifs/size/S-8.gif)
![S-9](gifs/size/S-9.gif)
![S-21](gifs/size/S-21.gif)
![S-22](gifs/size/S-22.gif)
![S-23](gifs/size/S-23.gif)
![S-24](gifs/size/S-24.gif)
![S-25](gifs/size/S-25.gif)
![S-26](gifs/size/S-26.gif)
![S-27](gifs/size/S-27.gif)
![S-28](gifs/size/S-28.gif)
![S-29](gifs/size/S-29.gif)
![S-2A](gifs/size/S-2A.gif)
![S-2B](gifs/size/S-2B.gif)
![S-2C](gifs/size/S-2C.gif)
![S-2D](gifs/size/S-2D.gif)
![S-2E](gifs/size/S-2E.gif)
![S-2F](gifs/size/S-2F.gif)
![S-3A](gifs/size/S-3A.gif)
![S-3B](gifs/size/S-3B.gif)
![S-3C](gifs/size/S-3C.gif)
![S-3D](gifs/size/S-3D.gif)
![S-3E](gifs/size/S-3E.gif)
![S-3F](gifs/size/S-3F.gif)
![S-40](gifs/size/S-40.gif)
![S-5B](gifs/size/S-5B.gif)
![S-5C](gifs/size/S-5C.gif)
![S-5D](gifs/size/S-5D.gif)
![S-5E](gifs/size/S-5E.gif)
![S-60](gifs/size/S-60.gif)
![S-7B](gifs/size/S-7B.gif)
![S-7C](gifs/size/S-7C.gif)
![S-7D](gifs/size/S-7D.gif)
![S-7E](gifs/size/S-7E.gif)
![S-a](gifs/size/S-a.gif)
![S-A](gifs/size/S-A.gif)
![S-b](gifs/size/S-b.gif)
![S-B](gifs/size/S-B.gif)
![S-c](gifs/size/S-c.gif)
![S-C](gifs/size/S-C.gif)
![S-d](gifs/size/S-d.gif)
![S-D](gifs/size/S-D.gif)
![S-e](gifs/size/S-e.gif)
![S-E](gifs/size/S-E.gif)
![S-f](gifs/size/S-f.gif)
![S-F](gifs/size/S-F.gif)
![S-g](gifs/size/S-g.gif)
![S-G](gifs/size/S-G.gif)
![S-h](gifs/size/S-h.gif)
![S-H](gifs/size/S-H.gif)
![S-i](gifs/size/S-i.gif)
![S-I](gifs/size/S-I.gif)
![S-j](gifs/size/S-j.gif)
![S-J](gifs/size/S-J.gif)
![S-k](gifs/size/S-k.gif)
![S-K](gifs/size/S-K.gif)
![S-l](gifs/size/S-l.gif)
![S-L](gifs/size/S-L.gif)
![S-m](gifs/size/S-m.gif)
![S-M](gifs/size/S-M.gif)
![S-n](gifs/size/S-n.gif)
![S-N](gifs/size/S-N.gif)
![S-o](gifs/size/S-o.gif)
![S-O](gifs/size/S-O.gif)
![S-p](gifs/size/S-p.gif)
![S-P](gifs/size/S-P.gif)
![S-q](gifs/size/S-q.gif)
![S-Q](gifs/size/S-Q.gif)
![S-r](gifs/size/S-r.gif)
![S-R](gifs/size/S-R.gif)
![S-s](gifs/size/S-s.gif)
![S-S](gifs/size/S-S.gif)
![S-t](gifs/size/S-t.gif)
![S-T](gifs/size/S-T.gif)
![S-u](gifs/size/S-u.gif)
![S-U](gifs/size/S-U.gif)
![S-v](gifs/size/S-v.gif)
![S-V](gifs/size/S-V.gif)
![S-w](gifs/size/S-w.gif)
![S-W](gifs/size/S-W.gif)
![S-x](gifs/size/S-x.gif)
![S-X](gifs/size/S-X.gif)
![S-y](gifs/size/S-y.gif)
![S-Y](gifs/size/S-Y.gif)
![S-z](gifs/size/S-z.gif)
![S-Z](gifs/size/S-Z.gif)

reversing this motion is easy
```
for m in {a..z} {A..Z} {0..9} ; do convert -reverse S-$m.gif R-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -reverse S-$m.gif R-$m.gif ; done
```

![R-0](gifs/size/R-0.gif)
![R-1](gifs/size/R-1.gif)
![R-2](gifs/size/R-2.gif)
![R-3](gifs/size/R-3.gif)
![R-4](gifs/size/R-4.gif)
![R-5](gifs/size/R-5.gif)
![R-6](gifs/size/R-6.gif)
![R-7](gifs/size/R-7.gif)
![R-8](gifs/size/R-8.gif)
![R-9](gifs/size/R-9.gif)
![R-21](gifs/size/R-21.gif)
![R-22](gifs/size/R-22.gif)
![R-23](gifs/size/R-23.gif)
![R-24](gifs/size/R-24.gif)
![R-25](gifs/size/R-25.gif)
![R-26](gifs/size/R-26.gif)
![R-27](gifs/size/R-27.gif)
![R-28](gifs/size/R-28.gif)
![R-29](gifs/size/R-29.gif)
![R-2A](gifs/size/R-2A.gif)
![R-2B](gifs/size/R-2B.gif)
![R-2C](gifs/size/R-2C.gif)
![R-2D](gifs/size/R-2D.gif)
![R-2E](gifs/size/R-2E.gif)
![R-2F](gifs/size/R-2F.gif)
![R-3A](gifs/size/R-3A.gif)
![R-3B](gifs/size/R-3B.gif)
![R-3C](gifs/size/R-3C.gif)
![R-3D](gifs/size/R-3D.gif)
![R-3E](gifs/size/R-3E.gif)
![R-3F](gifs/size/R-3F.gif)
![R-40](gifs/size/R-40.gif)
![R-5B](gifs/size/R-5B.gif)
![R-5C](gifs/size/R-5C.gif)
![R-5D](gifs/size/R-5D.gif)
![R-5E](gifs/size/R-5E.gif)
![R-60](gifs/size/R-60.gif)
![R-7B](gifs/size/R-7B.gif)
![R-7C](gifs/size/R-7C.gif)
![R-7D](gifs/size/R-7D.gif)
![R-7E](gifs/size/R-7E.gif)
![R-a](gifs/size/R-a.gif)
![R-A](gifs/size/R-A.gif)
![R-b](gifs/size/R-b.gif)
![R-B](gifs/size/R-B.gif)
![R-c](gifs/size/R-c.gif)
![R-C](gifs/size/R-C.gif)
![R-d](gifs/size/R-d.gif)
![R-D](gifs/size/R-D.gif)
![R-e](gifs/size/R-e.gif)
![R-E](gifs/size/R-E.gif)
![R-f](gifs/size/R-f.gif)
![R-F](gifs/size/R-F.gif)
![R-g](gifs/size/R-g.gif)
![R-G](gifs/size/R-G.gif)
![R-h](gifs/size/R-h.gif)
![R-H](gifs/size/R-H.gif)
![R-i](gifs/size/R-i.gif)
![R-I](gifs/size/R-I.gif)
![R-j](gifs/size/R-j.gif)
![R-J](gifs/size/R-J.gif)
![R-k](gifs/size/R-k.gif)
![R-K](gifs/size/R-K.gif)
![R-l](gifs/size/R-l.gif)
![R-L](gifs/size/R-L.gif)
![R-m](gifs/size/R-m.gif)
![R-M](gifs/size/R-M.gif)
![R-n](gifs/size/R-n.gif)
![R-N](gifs/size/R-N.gif)
![R-o](gifs/size/R-o.gif)
![R-O](gifs/size/R-O.gif)
![R-p](gifs/size/R-p.gif)
![R-P](gifs/size/R-P.gif)
![R-q](gifs/size/R-q.gif)
![R-Q](gifs/size/R-Q.gif)
![R-r](gifs/size/R-r.gif)
![R-R](gifs/size/R-R.gif)
![R-s](gifs/size/R-s.gif)
![R-S](gifs/size/R-S.gif)
![R-t](gifs/size/R-t.gif)
![R-T](gifs/size/R-T.gif)
![R-u](gifs/size/R-u.gif)
![R-U](gifs/size/R-U.gif)
![R-v](gifs/size/R-v.gif)
![R-V](gifs/size/R-V.gif)
![R-w](gifs/size/R-w.gif)
![R-W](gifs/size/R-W.gif)
![R-x](gifs/size/R-x.gif)
![R-X](gifs/size/R-X.gif)
![R-y](gifs/size/R-y.gif)
![R-Y](gifs/size/R-Y.gif)
![R-z](gifs/size/R-z.gif)
![R-Z](gifs/size/R-Z.gif)

<br>

## use multiple fonts
we can use multiple fonts in our for loop, i've included a few nerd fonts in the font folder of this repo, for the simplicity and ease of use the names have been removed for this following command and i only use the two digit numbers at the beginning
```
for i in {a..z} {A..Z} {0..9} ; for f in *.ttf ; do convert -gravity center -trim -background grey75 -fill grey25 -font ./$f -size 30x30 caption:$i -extent 30x30 $i-$f.jpg ; done
```
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for f in *.ttf ; do printf -v hex '%02X' $(( #char )) ; convert -gravity center -trim -background grey75 -fill grey25 -font ./$f -size 30x30 -extent 30x30 caption:$char $hex-$f.jpg ; done
```
convert the image sequences, using a longer delay of 16
```
for m in {a..z} {A..Z} {0..9} ; do convert -delay 16 $(ls -v $m-*.jpg) F-$m.gif ; done
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert -delay 16 $(ls -v $m-*.jpg) F-$m.gif ; done
```

![F-0](gifs/fonts/F-0.gif)
![F-1](gifs/fonts/F-1.gif)
![F-2](gifs/fonts/F-2.gif)
![F-3](gifs/fonts/F-3.gif)
![F-4](gifs/fonts/F-4.gif)
![F-5](gifs/fonts/F-5.gif)
![F-6](gifs/fonts/F-6.gif)
![F-7](gifs/fonts/F-7.gif)
![F-8](gifs/fonts/F-8.gif)
![F-9](gifs/fonts/F-9.gif)
![F-21](gifs/fonts/F-21.gif)
![F-22](gifs/fonts/F-22.gif)
![F-23](gifs/fonts/F-23.gif)
![F-24](gifs/fonts/F-24.gif)
![F-25](gifs/fonts/F-25.gif)
![F-26](gifs/fonts/F-26.gif)
![F-27](gifs/fonts/F-27.gif)
![F-28](gifs/fonts/F-28.gif)
![F-29](gifs/fonts/F-29.gif)
![F-2A](gifs/fonts/F-2A.gif)
![F-2B](gifs/fonts/F-2B.gif)
![F-2C](gifs/fonts/F-2C.gif)
![F-2D](gifs/fonts/F-2D.gif)
![F-2E](gifs/fonts/F-2E.gif)
![F-2F](gifs/fonts/F-2F.gif)
![F-3A](gifs/fonts/F-3A.gif)
![F-3B](gifs/fonts/F-3B.gif)
![F-3C](gifs/fonts/F-3C.gif)
![F-3D](gifs/fonts/F-3D.gif)
![F-3E](gifs/fonts/F-3E.gif)
![F-3F](gifs/fonts/F-3F.gif)
![F-40](gifs/fonts/F-40.gif)
![F-5B](gifs/fonts/F-5B.gif)
![F-5C](gifs/fonts/F-5C.gif)
![F-5D](gifs/fonts/F-5D.gif)
![F-5E](gifs/fonts/F-5E.gif)
![F-60](gifs/fonts/F-60.gif)
![F-7B](gifs/fonts/F-7B.gif)
![F-7C](gifs/fonts/F-7C.gif)
![F-7D](gifs/fonts/F-7D.gif)
![F-7E](gifs/fonts/F-7E.gif)
![F-a](gifs/fonts/F-a.gif)
![F-A](gifs/fonts/F-A.gif)
![F-b](gifs/fonts/F-b.gif)
![F-B](gifs/fonts/F-B.gif)
![F-c](gifs/fonts/F-c.gif)
![F-C](gifs/fonts/F-C.gif)
![F-d](gifs/fonts/F-d.gif)
![F-D](gifs/fonts/F-D.gif)
![F-e](gifs/fonts/F-e.gif)
![F-E](gifs/fonts/F-E.gif)
![F-f](gifs/fonts/F-f.gif)
![F-F](gifs/fonts/F-F.gif)
![F-g](gifs/fonts/F-g.gif)
![F-G](gifs/fonts/F-G.gif)
![F-h](gifs/fonts/F-h.gif)
![F-H](gifs/fonts/F-H.gif)
![F-i](gifs/fonts/F-i.gif)
![F-I](gifs/fonts/F-I.gif)
![F-j](gifs/fonts/F-j.gif)
![F-J](gifs/fonts/F-J.gif)
![F-k](gifs/fonts/F-k.gif)
![F-K](gifs/fonts/F-K.gif)
![F-l](gifs/fonts/F-l.gif)
![F-L](gifs/fonts/F-L.gif)
![F-m](gifs/fonts/F-m.gif)
![F-M](gifs/fonts/F-M.gif)
![F-n](gifs/fonts/F-n.gif)
![F-N](gifs/fonts/F-N.gif)
![F-o](gifs/fonts/F-o.gif)
![F-O](gifs/fonts/F-O.gif)
![F-p](gifs/fonts/F-p.gif)
![F-P](gifs/fonts/F-P.gif)
![F-q](gifs/fonts/F-q.gif)
![F-Q](gifs/fonts/F-Q.gif)
![F-r](gifs/fonts/F-r.gif)
![F-R](gifs/fonts/F-R.gif)
![F-s](gifs/fonts/F-s.gif)
![F-S](gifs/fonts/F-S.gif)
![F-t](gifs/fonts/F-t.gif)
![F-T](gifs/fonts/F-T.gif)
![F-u](gifs/fonts/F-u.gif)
![F-U](gifs/fonts/F-U.gif)
![F-v](gifs/fonts/F-v.gif)
![F-V](gifs/fonts/F-V.gif)
![F-w](gifs/fonts/F-w.gif)
![F-W](gifs/fonts/F-W.gif)
![F-x](gifs/fonts/F-x.gif)
![F-X](gifs/fonts/F-X.gif)
![F-y](gifs/fonts/F-y.gif)
![F-Y](gifs/fonts/F-Y.gif)
![F-z](gifs/fonts/F-z.gif)
![F-Z](gifs/fonts/F-Z.gif)

<br>

## change character position
with every example so far we've been trying to keep the character at the center of the image using `-gravity center` but we can change the position and make a motion out of it, the -gravity flags takes 9 alignment positions using center, north, northeast and etc, so lets loop all of the 9 positions in a for loop
```
for i in {a..z} {A..Z} {0..9} ; for g in northwest north northeast west center east southwest south southeast ; do convert -gravity $g -trim -background green -fill yellow -font ./nerd.ttf -size 30x30 caption:$i -extent 30x30 $i-$g.jpg ; done
```
```
for char in {\!..\)} \@ \` {\*..\/} {\:..\?} {\[..\^} {\{..\~} ; for g in northwest north northeast west center east southwest south southeast ; do printf -v hex '%02X' $(( #char )) ; convert -gravity $g -trim -background green -fill yellow -font ./nerd.ttf -size 30x30 -extent 30x30 caption:$char $hex-$g.jpg ; done
```
these two commands give us the character and the position they are after as filenames

| northwest | north | northeast |
|---|---|---|
| ![](temp/A-northwest.jpg) | ![](temp/A-north.jpg) | ![](temp/A-northeast.jpg) |
| west | center | east |
| ![](temp/A-west.jpg) | ![](temp/A-center.jpg) | ![](temp/A-east.jpg) |
| southwest | south | southeast |
| ![](temp/A-southwest.jpg) | ![](temp/A-south.jpg) | ![](temp/A-southeast.jpg) |

now we need to decide the direction of our motion and change these filenames accordingly, i want a normal clockwise motion from northwest to west so we'll rename these files one by one and pad the next number after them, here is the first example which changes every filename that has northwest in it to 1 which is the first frame in each of our gifs
```
for i in *-northwest.jpg ; do mv "$i" "${i/northwest/1}" ; done
```
same command can be used for the next positions, or better yet, do it all in one giant command!
```
for i in *-northwest.jpg ; do mv "$i" "${i/northwest/1}" ; done 
for i in *-north.jpg ; do mv "$i" "${i/north/2}" ; done
for i in *-northeast.jpg ; do mv "$i" "${i/northeast/3}" ; done
for i in *-east.jpg ; do mv "$i" "${i/east/4}" ; done
for i in *-southeast.jpg ; do mv "$i" "${i/southeast/5}" ; done
for i in *-south.jpg ; do mv "$i" "${i/south/6}" ; done
for i in *-southwest.jpg ; do mv "$i" "${i/southwest/7}" ; done
for i in *-west.jpg ; do mv "$i" "${i/west/8}" ; done
```
we take the opportunity to remove the unwanted center pictures since we don't need them anymore, depending on the motion you desire you might want to keep these or remove even more of these positions or don't even include them in your for loops
```
rm *-center.jpg
```
now convert these images to gifs
```
for m in {a..z} {A..Z} {0..9} ; do convert $(ls -v $m-*.jpg) ge-$m.gif ; done 
```
```
for m in 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F 3A 3B 3C 3D 3E 3F 40 5B 5C 5D 5E 60 7B 7C 7D 7E ; do convert $(ls -v $m-*.jpg) ge-$m.gif ; done
```

![ge-0](gifs/gravity/ge-0.gif)
![ge-1](gifs/gravity/ge-1.gif)
![ge-2](gifs/gravity/ge-2.gif)
![ge-3](gifs/gravity/ge-3.gif)
![ge-4](gifs/gravity/ge-4.gif)
![ge-5](gifs/gravity/ge-5.gif)
![ge-6](gifs/gravity/ge-6.gif)
![ge-7](gifs/gravity/ge-7.gif)
![ge-8](gifs/gravity/ge-8.gif)
![ge-9](gifs/gravity/ge-9.gif)
![ge-21](gifs/gravity/ge-21.gif)
![ge-22](gifs/gravity/ge-22.gif)
![ge-23](gifs/gravity/ge-23.gif)
![ge-24](gifs/gravity/ge-24.gif)
![ge-25](gifs/gravity/ge-25.gif)
![ge-26](gifs/gravity/ge-26.gif)
![ge-27](gifs/gravity/ge-27.gif)
![ge-28](gifs/gravity/ge-28.gif)
![ge-29](gifs/gravity/ge-29.gif)
![ge-2A](gifs/gravity/ge-2A.gif)
![ge-2B](gifs/gravity/ge-2B.gif)
![ge-2C](gifs/gravity/ge-2C.gif)
![ge-2D](gifs/gravity/ge-2D.gif)
![ge-2E](gifs/gravity/ge-2E.gif)
![ge-2F](gifs/gravity/ge-2F.gif)
![ge-3A](gifs/gravity/ge-3A.gif)
![ge-3B](gifs/gravity/ge-3B.gif)
![ge-3C](gifs/gravity/ge-3C.gif)
![ge-3D](gifs/gravity/ge-3D.gif)
![ge-3E](gifs/gravity/ge-3E.gif)
![ge-3F](gifs/gravity/ge-3F.gif)
![ge-40](gifs/gravity/ge-40.gif)
![ge-5B](gifs/gravity/ge-5B.gif)
![ge-5C](gifs/gravity/ge-5C.gif)
![ge-5D](gifs/gravity/ge-5D.gif)
![ge-5E](gifs/gravity/ge-5E.gif)
![ge-60](gifs/gravity/ge-60.gif)
![ge-7B](gifs/gravity/ge-7B.gif)
![ge-7C](gifs/gravity/ge-7C.gif)
![ge-7D](gifs/gravity/ge-7D.gif)
![ge-7E](gifs/gravity/ge-7E.gif)
![ge-a](gifs/gravity/ge-a.gif)
![ge-A](gifs/gravity/ge-A.gif)
![ge-b](gifs/gravity/ge-b.gif)
![ge-B](gifs/gravity/ge-B.gif)
![ge-c](gifs/gravity/ge-c.gif)
![ge-C](gifs/gravity/ge-C.gif)
![ge-d](gifs/gravity/ge-d.gif)
![ge-D](gifs/gravity/ge-D.gif)
![ge-e](gifs/gravity/ge-e.gif)
![ge-E](gifs/gravity/ge-E.gif)
![ge-f](gifs/gravity/ge-f.gif)
![ge-F](gifs/gravity/ge-F.gif)
![ge-g](gifs/gravity/ge-g.gif)
![ge-G](gifs/gravity/ge-G.gif)
![ge-h](gifs/gravity/ge-h.gif)
![ge-H](gifs/gravity/ge-H.gif)
![ge-i](gifs/gravity/ge-i.gif)
![ge-I](gifs/gravity/ge-I.gif)
![ge-j](gifs/gravity/ge-j.gif)
![ge-J](gifs/gravity/ge-J.gif)
![ge-k](gifs/gravity/ge-k.gif)
![ge-K](gifs/gravity/ge-K.gif)
![ge-l](gifs/gravity/ge-l.gif)
![ge-L](gifs/gravity/ge-L.gif)
![ge-m](gifs/gravity/ge-m.gif)
![ge-M](gifs/gravity/ge-M.gif)
![ge-n](gifs/gravity/ge-n.gif)
![ge-N](gifs/gravity/ge-N.gif)
![ge-o](gifs/gravity/ge-o.gif)
![ge-O](gifs/gravity/ge-O.gif)
![ge-p](gifs/gravity/ge-p.gif)
![ge-P](gifs/gravity/ge-P.gif)
![ge-q](gifs/gravity/ge-q.gif)
![ge-Q](gifs/gravity/ge-Q.gif)
![ge-r](gifs/gravity/ge-r.gif)
![ge-R](gifs/gravity/ge-R.gif)
![ge-s](gifs/gravity/ge-s.gif)
![ge-S](gifs/gravity/ge-S.gif)
![ge-t](gifs/gravity/ge-t.gif)
![ge-T](gifs/gravity/ge-T.gif)
![ge-u](gifs/gravity/ge-u.gif)
![ge-U](gifs/gravity/ge-U.gif)
![ge-v](gifs/gravity/ge-v.gif)
![ge-V](gifs/gravity/ge-V.gif)
![ge-w](gifs/gravity/ge-w.gif)
![ge-W](gifs/gravity/ge-W.gif)
![ge-x](gifs/gravity/ge-x.gif)
![ge-X](gifs/gravity/ge-X.gif)
![ge-y](gifs/gravity/ge-y.gif)
![ge-Y](gifs/gravity/ge-Y.gif)
![ge-z](gifs/gravity/ge-z.gif)
![ge-Z](gifs/gravity/ge-Z.gif)

<br>

###### more examples coming soon
