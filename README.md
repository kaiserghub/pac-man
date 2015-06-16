# Pac-Man in < 512 Bytes of HTML+JS

Based on the the [oldskool remake by @maettig ](http://maettig.com/code/javascript/pac-man-in-140byt.es.html) of the classic arcade game Pac-Man. Golfed down by @aemkei, @p01, @subzey, @xem, @0ndras, @maettig. See the original [gist](https://gist.github.com/maettig/1384306).

### Demo

[PLAY THE DEMO](http://output.jsbin.com/hitige/quiet)!

Use your keyboard to control the movement.

### Source (402 Bytes)

```html
<pre id=p><script>l="";for(i in L=[a=8191,b=4161,c=5981,d=5125
,5493,5397,5589,d,c,b,a])l+=L[i].toString(2)+3;l=l.split(""),w
=14,x=76,X=48,d=k=D=!setInterval(onkeydown=function(n){if(k=n?
n.which-38:k,!n&&x^X)for(l[x]=2,l[x+=d=k+1>>2||1&l[x+(o=k%2?k:
k*w-w)]?1&l[x+d]?0:d:o]=4,l[X]&=7,b=D%4,b=b%2?b-2:(b-1)*w,1&l[
X+b]?D++:X+=b,l[X]|=8,h=i=0;153>i;)h+=".# \no   x"[l[++i]]||"x
";p.innerHTML=h},250)</script>
```

### Gameplay Video

![Pac-Man](https://raw.githubusercontent.com/codegolf/pac-man/master/pacman.gif)

### Board Layout

```
#############
#     #    .#       #   = Wall
# ### # ###.#
# # X    .#.#       X   = Ghost
# # # ###.#.#
# # # o #.#.#       o   = Player
# # ### #.#.#
# # ......#.#       .   = Gold
# ### #.###.#
#.....#.....#
#############
```

### Annotated Source

```html
<pre id=p><script>
l = "";
for (i in L = [
  a = 8191,                               // #############
  b = 4161,                               // #     #     #
  c = 5981,                               // # ### # ### #
  d = 5125,                               // # #       # #
  5493,                                   // # # # ### # #
  5397,                                   // # # #   # # #
  5589,                                   // # # ### # # #
  d,                                      // # #       # #
  c,                                      // # ### # ### #
  b,                                      // #     #     #
  a                                       // #############
]
) l += L[i]
  .toString(2)                            // convert to binary
  + 3;                                    // placeholder for \n

l = l.split(""),

w = 14,                                   // width
x = 76,                                   // players x position
X = 48,                                   // ghost x position

d =                                       // player direction
k =                                       // last keycode
D = !                                     // ghost direction

setInterval(onkeydown = function(a) {

  k = a ? a.which - 38 : k;               // get key code

  if (
    !a &&                                 // skip on key press
    x ^ X                                 // check ghost and player collission
  ) for (

    l[x] = 2,                             // reset cell
    l[
      x += d = k + 1 >> 2 || 1 & l[       // update player direction
        x + (                             // update player position
          o =                             // calculate offset
            k % 2 ?                       // horizontal or vertical movement
              k  :                        // = horizontal
              k * w - w                   // = vertical
        )
      ] ? 1 & l[x + d] ? 0 : d : o        // detect wall collision
    ] = 4,                                // set player at new position
    l[X] &= 7,                            // remove ghost first

    b = D % 4,
    b = b % 2 ? b - 2 : (b - 1) * w,      // calculate walking direction
    1 & l[X + b]                          // if walking into a wall
      ? D++                               // rotate ghost by 90 degree
      : X += b                            // else walk
      ,
      l[X] |= 8,                           // place ghost

      h = i = 0;
      153 > i;
  )
    h += ".# \no   x"                     // 0 = . = empty
                                          // 1 = o = player
                                          // 2 = . = gold
                                          // 4 = # = wall
                                          // 8 = x = ghost
                                          // 3 = \n placeholder
     [l[++i]] || "x"                      // get character


  p.innerHTML = h
}, 250)
</script>
```
