java c
ICS   33 Fall   2024
Project   4: Still   Looking   for   Something
Due   date   and   time:   Wednesday, November   27, 11:59pm
Git   repository:
https://ics.uci.edu/~thornton/ics33/ProjectGuide/Project4/Project4.git
Background
Our   recent   discussion   of   Functional   Programming   alluded   to   the   fact   that   what   makes
programming   languages   different   from   one   another   isn't   solely   their   syntax, though
that's   certainly   part   of   it. Each   programming   language   asks   its   users   to   think   differently — sometimes   dramatically   so   — about   how   best   to   organize   our   solution   to   a   problem.
What's   considered   normal   (or   even   desirable) in   an   object-oriented   language   might   be          awkward   (or   even   impossible) in   a   purely   functional   language,   and   vice   versa.   How   we'd   solve   a   problem   in   a   data   manipulation   language   like   SQL   would   be   radically   different
from   how   we'd   solve   the   same   problem   in   a   language   like   Python. Naturally,   some   kinds of   problems   will   be   better   solved   with   one   set   of   tools   than   another, so   we'd   expect
different   programming   languages   to   excel   at   different   tasks; part   of   why   we   want   some       exposure   to   more   than   one   programming   language   is   so   that   we   can   start   to   develop   our sensibilities   about   the   ways   that   languages   can   differ, and   how   we   might   be   able   to
recognize   the   kinds   of   problems   that   are   a   better   fit   for   some   than   others. That   way,   even if   we   don't   become   experts   in   multiple   languages   at   once, we'll   at   least   have   embraced
the   idea   that   no   single   language   is   the   best   solution   to   every   problem; that'll   open   our
minds   to   learning   about   alternatives   when   they   show   promise, rather   than   falling   in   love   with   our   first   language   and   never   being   able   to   let   go   of   it,   or   simply   riding   the   waves   of       hype   and   fashion   wherever   they   lead, for   better   or   worse.
Fortunately, we've   already   had   a   head   start   on   that   journey, because   Project   2   asked   you to   build   a   single   application   that   was   written   using   more   than   one   programming
language. We   used   Python   to   implement   our   user   interface   and   the   "engine"   underlying it, while   we   instead   used   SQL   to   describe   our   interactions   with   the   database   that   stored    and   managed   the   program's   data. The   technique   of   writing   systems   made   up   of   code
written in multiple programming languages is sometimes calledpolyglot   programming,   which, like   many   choices   we   make   in   computing, represents   a   tradeoff: We   give   up   the             simplicity   of   writing   everything   in   a   single   language, but   we   gain   access   to   a   set   of
abilities   that   approach   the   union   of   the   abilities   of   all   of   the   languages   we're   using. As          long   as   we   can   figure   out   how   to   make   code   in   one   language   work   together   with   code   in another   — in   Project   2, we   relied   on   the      sqlite3   library   to   smoothly   communicate   between   them   — and   as   long   as   we're   careful   to   use   the   "best-fit"   language   for   each   part          of   our   program, we   can   sometimes   achieve   things   that   are   much   more   difficult   to   achieve when   writing   everything   in   one   language. The   more   complex   the   system, the   greater   the       chance   it   may   benefit   from   polyglot   techniques.
Among   the   differences   between   programming   languages   are   the   differences   in   their
syntax, which   is   to   say   that   different   programming   languages   allow   us   to   use   different   keywords   and   symbols   in   different   orders. Where   a   SQL   statement   might   begin   with
SELECT   or   CREATE   TABLE, a   Python   statement   might   instead   begin   with      class   or   def.   There   is   some   overlap   between   the   words   and   phrases   allowed   across   programming
languages, but   there   are   almost   always   differences   somewhere. We   can   write      a   + bin   both   Python   and   SQL, for   example, but   the   statements   in   which   it   can   legally   appear             would   need   to   be   structured   differently.
As   you'll   see   in   later   coursework, the   ability   to   describe   the   syntax   of   a   programming
language   is   a   fairly   universal   need, so   we   would   benefit   from   understanding   a   universal solution   to   it. A   grammar   is   a   well-known   formalism   that   can   do   that   job   nicely.
Grammars   provide   a   formal   way   to   describe   syntax, allowing   us   to   specify   the   valid
orders   in   which   words   and   symbols   can   appear. Grammars   form   the   theoretical   basis   of parsers   like   the   one   provided   in   Project   3, whose   main   jobs   are   to   decide   whether   a
sequence   of   symbols   is   valid, by   inferring   the   structure   from   which   it   derives   its
meaning. But   we   can   use   grammars   in   the   opposite   direction, too   — generating          sequences   of   symbols   that   we   know   are   valid, rather   than   determining   whether   a   sequence   of   symbols   is   valid   — and   that's   our   focus   in   this   project.
To   satisfy   this   project's   requirements, you'll   write   a   program   that   randomly   generates
text   in   accordance   with   a   grammar   that's   given   as   the   program's   input.   (Note   that
parsing   and   generating   text   are   hardly   the   only   tasks   for   which   we   can   use   grammars;
they're   recurrent   in   the   study   of   computer   science, so   you're   likely   to   see   them   again   in
your   studies, probably   more   than   once.) You   will   also   gain   practice   implementing   a
mutually   recursive   algorithm   in   Python, which   will   strengthen   your   understanding   of   our   recent   conversation   in   which   we   were   Revisiting   Recursion.
Grammars
A   grammar   is   a   collection   of   substitution   rules, each   of   which   specifies   how   a   symbol
can   be   replaced   with   a   sequence   of   other   symbols. Collectively, the   substitution   rules   that comprise   a   grammar   describe   a   set   of   sentences   that   we   say   make   up   a   language.
As   a   first   example, consider   the   following   grammar.
A   →   0 A   1 A   | B   B   →   #
There   are   two   rules   that   make   up   our   grammar:   One   specifying   how   the   symbol   A   can   be replaced, and   another   specifying   a   different   replacement   for   B. We   say   that   symbols   that can   be   replaced   in   this   way   are   variables, which   I've   denoted   here   with   boldfaced,   underlined   text. Meanwhile, we   say   that   symbols   that   cannot   be   replaced   are   terminals,         and   that   the   sentences   that   are   part   of   a   language   described   by   a   grammar   are   made   up only   of   terminals. There   are   two   variables   in   our   grammar   (A   and   B)   and   three   terminals (0,   1,   and   #).
The   vertical   bar   ('   |') symbol   in   the   rule   for   A   indicates   optionality, which   is   to   say   that   we can   replace   an   occurrence   of   A   with   one   of   two   options:   either   with   the   symbols   0 A   1 A            or   with   the   symbol   B. Lacking   a   vertical   bar, the   rule   for   B   offers   only   one   option: We
can   only   replace   B   with   the   terminal   #.
We   consider   one   of   the   variables   to   be   the   start   variable, which   is   meant   to   describe   an entire   sentence. Other   variables   describe   fragments   of   sentences. For   the   purposes   of this   example, we'll   say   that   A   is   the   start   variable.
Generating   a   sentence   from   a   grammar
From   a   conceptual   point   of   view, a   grammar   can   be   used   to   generate   strings   of   terminals within   its   language   in   the   following   manner. (I   should   point   out   that   this   will   not   be
precisely   how   your   program   will   generate   its   output, but   we'll   starthere, since   it's   a   good   way   to   understand   the   concepts   underlying   what   we're   doing.)
1. Begin   with   a   sentence   containing   only   one   symbol: the   start   variable.
2. As   long   as   there   are   still   variables   in   the   sentence, pick   one   of   them,   find   the
corresponding   rule   with   that   variable   on   its   left-hand   side, and   choose   one   of   its options. Replace   the   variable   with   the   symbols   in   the   option   you   chose.
A   sequence   of   substitutions   leading   from   the   start   variable   to   a   string   of   terminals   is called   a   derivation. When   the   leftmost   variable   is   always   replaced   at   each   step,   the
derivation is called a leftmost derivation. The sentence   0   0   #   1   #   1   #   is   in   the   language described   by   the   grammar   above, a   fact   we   can   prove   using   the   following   leftmost derivation.
A   ⇒   0 A   1 A   ⇒   0   0 A   1 A   1 A   ⇒   0   0 B   1 A   1 A   ⇒   0   0   #   1 A   1 A   ⇒   0   0   #   1 B   1 A   ⇒   0   0   #   1   #   1 A   ⇒   0   0   #   1   #   1 B   ⇒   0   0   #   1   #   1   #
The   algorithm   described   above   would   be   able   to   produce   this   same   sentence   by   making the   same   choices   for   each   application   of   a   rule   that   was   made   in   this   derivation.
We   would   say, generally, that   the   language   of   a   grammar   is   the   set   of   all   strings   of
terminals   for   which   such   a   derivation   can   be   built. It's   worth   noting   that   there   are   two aspects   of   this   problem   where   infiniteness   comes   into   play.
·      The   set   of   strings   in   a   language   maybe   infinite. For   example,   if   a   grammar
contained   the   rule   X   → 1 X   |   1, there   would   be   no   limit   on   how   many   times   we
could   choose   the   1 X   option   instead   of   the   1 option. Still,   if   we're   generating   strings at   random, we'll   always   pick   exactly   one   of   these   options,   and   we   expect,   sooner   or   later, to   choose   the   1 option, which   would   prevent   the   generated   string   from becoming   any   longer.
·    A   grammar   can   be   written   in   a   way   that   it   describes   individual   strings   of   infinite
length. If   the   only   choice   for   the   symbol   Y   is   the   rule   Y   → 1 Y, a   derivation   in   which a   string   contains   Y   will   never   end; any   substitution   based   on   that   rule   will   still   lead    to   a   string   containing   Y. (This   is   a   similar   problem   we   encounter   when   we   have   a
recursive   function   with   no   base   case.) In   practice, though, a   properly   written   grammar   will   eventually   lead   only   to   sentences   of   finite   length.
The   program
The   basic   goal   of   your   program   is   to   use   the   description   of   a   grammar   to   randomly
generate   sentences   that   are   in   the   grammar's   language. There   are   a   number   of   details   to consider, which   are   described   below.
The   format   of   a   grammar   file
The   program   will   read   a   grammar   file, which   contains   the   description   of   a   grammar   to be   used   for   generating   random   sentences. To   include   that   feature   in   your   program,
though, we'll   need   to   agree   on   a   format   for   grammar   files, which   is   specified   in   detail below.
·      Each   rule   starts   with   a   line   containing   only   a   left   curly   brace      {. We'll   say   that   each of   these   lines   is   called   a   rule   opener.
·      Each   rule   ends   with   a   line   containing   only   a   right   curly   brace      }. We'll   say   that   each of   these   lines   is   called   a   rule   closer.
·    Any   line   of   text   that   is   not   between   a   rule   opener   and   a   subsequent   rule   closer   is             considered   to   be   a   comment   (i.e., it's   irrelevant   from   our   perspective, but   can   be   a    useful   way   to   write   a   grammar   file   that   would   be   more   understandable   to   a   human   reader).
·    After   a   rule   opener,   the   next   line   specifies   the   name   of   the   variable   for   which   a   rule       is   being   described. This   line   will   consist   of   only   letters   and   digits, but   no   whitespace (or   other) characters.
·      Subsequent   lines   of   the   rule   are   the   options   for   substituting   a   sequence   of   symbols in   place   of   the   rule's   variable. There   will   always   be   at   least   one   of   these   lines,   and          each   of   them   will   be   as   follows.
o         It   will   begin   with   a   positive   integer   (i.e.,   an   integer   greater   than   zero) that
specifies   the   option's   weight, which   determineshow   frequently   we'll   choose   it,   relative   to   the   others. That   weight   will   be   followed   by   a   space.
。After   that   will   be   zero   or   more   symbols, each   adjacent   pair   separated   by   a
single   space. When   a   symbol   consists   of   letters   and   digits   surrounded   by
brackets   (i.e.,    [   and      ]), it   is   a   variable; otherwise, it   is   a   terminal.   (Note   that the   syntactic   meaning   of   spaces   means   that   symbols   cannot   contain   spaces.)
As   we'll   see, a   grammar   file   doesn't   specify   a   start   variable; that's   specified   subsequently as   input   to   the   program, so   that   the   same   grammar   fil代 写ICS 33 Fall 2024 Project 4: Still Looking for SomethingPython
代做程序编程语言e   can   be   used   with   different   start   variables   in   different   runs.
Having   seen   a   description   of   the   format, let's   take   a   look   at   an   example   grammar   file,   so we   can   fully   understand   the   details   of   what   it   means.
{
HowIsBoo
1 Boo   is   [Adjective]   today   }
{
Adjective   3   happy
3   perfect
1   relaxing
1 fulfilled
2   excited   }
Let's   suppose   that   HowIsBoo   is   the   start   variable. If   so, then   the   grammar   describes sentences   whose   basic   structure   is   always      Boo   is                     today, with   the                                                   replaced   with   one   of   five   adjectives:
·      There's   a   3-in-10 (30%) chance   of   the   adjective   being      happy.
·      There's   a   3-in-10 (30%) chance   of   the   adjective   being      perfect.      ·      There's   a   1-in-10 (10%) chance   of   the   adjective   being      relaxing.
·      There's   a   1-in-10 (10%) chance   of   the   adjective   being   fulfilled.   ·      There's   a   2-in-10 (20%) chance   of   the   adjective   being   excited.
Where   did   those   probabilities   come   from? The   sum   of   the   weights   for   all   of   the   options for the   Adjective   variable is   10.   (3   + 3   +   1   +   1   +   2   =   10.) Each individual weight is   a
numerator, and   that   sum   is   the   denominator;    happy   has   a   weight   of   3, so   its   odds   are   3-   in-10   (30%), and so   on.
One   thing   this   example   demonstrates   is   that   weights   have   no   meaning   across   rules, but only   within   a   rule. For   example, the   sum   of   the   weights   in   the   rule   for   HowIsBoo   is   1,
while   the   sum   for   Adjective   is   10, which   means   that   "1 point" of   weight   means   more   in the   HowisBoo   rule   than   it   does   in   the   Adjective   rule.
A   more   complete   example   grammar   file
To   provide   you   with   a   more   complete   example   of   a   grammar   file,   check   out   the   example linked   below.
·      grin.txt
That's   a   grammar   file   that, when   its   start   variable   is   GrinStatement, generates   random statements   written   in   the   Grin   language   from   Project   3. The   generated   statements   will
have   no   syntax   errors   in   them, so   it   should   be   possible   to   run   the   lexer   and   parser   on
them; however, since   the   statements   are   generated   individually   and   separately, it's
unlikely   that   you'd   be   able   to   run   them   as   a   Grin   program, because   they   may   have   run-
time   errors   or   other   problems, such   as   infinite   loops,   division   by   zero, or   jumping   to   non-   existent   labels. Generating   semantically   valid   Grin   programs   (i.e., ones   that   you   could
successfully   execute) is   a   problem   that   grammars   are   not   equipped   to   solve,   as   it   turns out.
The   input
The   program   will   begin   by   reading   exactly   three   lines   from   the   Python   shell   (i.e.,   using Python's   built-in   input   function).
1. The   path   to   an   existing   grammar   file. (If   only   the   name   of   the   file   is   specified,   it   will need   to   be   located   in   the   program's   current   working   directory, which, by   default, is   the   same   directory   as   your   main   module.)
2. A   positive   integer   specifying   the   number   of   random   sentences   to   be   generated.   (Note   that, as   always, zero   is   not   a   positive   number.)
3. The   name   of   the   start   variable. (A   variable's   name   does   not   include   the   brackets;   the brackets   are   a   syntactic   device   within   the   grammar   file   to   make   clear   when   an
option   is   referring   to   a   variable.)You   can   safely   assume   that   the   grammar   file   exists, that   it   will   be   valid   (i.e., it   will   follow the   grammar   file   format   described   above), and   that   the   program   input   will   be   formatted      according   to   the   rules   specified   here; we   won't   be   testing   your   program   with   inputs   that         don't   meet   those   requirements, so   your   program   can   do   anything   (or   even   crash) if   given such   inputs.
We   also   will   not   be   testing   with   a   grammar   file   that   describes   infinite-length   sentences,            which   means   that   your   program   can   do   anything   (or   even   crash)   if   given   such   a   grammar file.
The   output
The   output   of   your   program   is   simple: If   asked   to   generate   n   sentences, your   program would   print   a   total   of   n   lines   of   output, each   being   one   of   those   sentences,   and   each having   a   newline   on   the   end   of   it. No   more,   no   less.
Each   sentence   is   a   sequence   of   terminals, separated   by   spaces.   That's   it.
A   complete   example   of   the   program's   execution
Let's   suppose   that   we   had   a   grammar   file   named   grammar.txt   identical   to   the   shorter example   shown   above. Given   that, an   example   of   the   program's   execution   might   look   like this.
grammar.txt 10
HowIsBoo
Boo   is happy   today
Boo   is   fulfilled   today Boo   is relaxing   today      Boo   is excited   today         Boo   is   perfect   today       Boo   is happy   today
Boo   is   perfect   today Boo   is   perfect   today Boo   is excited   today   Boo   is happy   today
Don't   forget   that   the   output   is   generated   randomly, which   means   that   a   subsequent   run       of   the   same   program   with   the   same   grammar   file   and   the   same   input   might   reasonably be   expected   to   produce   different   output. Remember, too, that   the   grammar   file   specifies    its   options   as   weights   that   are   probabilities   rather   than   being   absolute.   Consequently,   a subsequent   run   that   generates   10 sentences   may, for   example, have   a   different   number          of   occurrences   Boo   is   happy   today;just   because   there's   a   3-in-10 chance   that      happy    is   chosen   in   each   sentence   doesn't   mean   that   exactly   three   out   of   every   ten   sentences   will contain   happy.   (You   can   flip   a   coin   ten   times   in   a   row   and   it   can   come   up   heads   all   ten times, even   though   there's   a   1-in-2 chance   of   it   happening   each   time.   It's   not   likely, but   it's   not   impossible, either.)
Design   requirements
There   are   a   number   of   ways   that   this   problem   could   be   solved, but   we'll   focus   on   an
approach   that   leads   to   a   clean, mutually   recursive   algorithm   for   solving   it, which   you'll be   required   to   implement.
Representing   the   grammar   as   objects
From   the   description   of   the   grammar   file, we   can   see   that   it's   built   up   from   the   following concepts.
·    A   grammar   contains   a   collection   of   rules.
·      Each   rule   is   made   up   of   a   variable   and   one   or   more   options.
·      Each   option   has   a   weight   and   a   sequence   of   symbols,   each   of   which   is   a   terminal   or a   variable.
These   facts   lead   directly   to   an   idea   of   how   to   design   a   combination   of   objects   that   can   be used   to   represent   a   grammar.
·    A   class   representing   a   terminal   symbol.   ·    A   class   representing   a   variable   symbol.
·      A   class   representing   an   option.   ·      A   class   representing   a   rule.
·    A   class   representing   a   grammar.
This   may   seem   like   a   heavy-handed   approach, but   it   pays   off   if   we   take   it   a   step   further.    What   if   all   of   these   classes   implemented   the   same   protocol, which   allows   us   to   ask   any   of their   objects   to   do   the   same   job: "Given   this   grammar,   generate   a   sentence   fragment
from   yourself"?
Generating   random   sentences   from   a   grammar
Once   you've   represented   your   grammar   as   a   combination   of   objects   as   described   in   the previous   section, it   is   possible   to   implement   a   relatively   straightforward   mutually
recursive   algorithm   to   generate   random   sentences   from   it. The   algorithm   revolves
around   the   idea   of   generating   sentence   fragments, then   putting   the   fragments   together into   a   complete   sentence.
Here   is   a   sketch   of   such   an   algorithm.
·      To   generate   a   sentence   from   a   grammar, it   will   look   up   the   rule   corresponding   to the   start   variable, then   ask   that   rule   to   generate   a   sentence   fragment.
·      To   generate   a   sentence   fragment   from   a   rule,   one   of   its   options   will   be   chosen   at          random   (in   accordance   with   their   weights), which   will   then   be   asked   to   generate   a   sentence   fragment.
·      To   generate   a   sentence   fragment   from   an   option,   iterate   through   its   symbols,   generating   sentence   fragments   from   each   one.
·      To   generate   a   sentence   fragment   from   a   variable   symbol,   ask   the   grammar   for   the rule   corresponding   to   that   variable, then   ask   that   rule   to   generate   a   sentence
fragment.
·      To   generate   a   sentence   fragment   from   a   terminal   symbol, yield   only   the   value   of that   terminal; that's   its   sentence   fragment.
This   mutually   recursive   strategy   provides   a   great   deal   of   power   with   relatively   little   code;   by   relying   on   Python's   duck   typing   mechanism, we   can   allow   the   "right   thing" to   happen   quickly   and   easily. (Note   that   why   we   say   it's   a   "mutually   recursive"   strategy   is   because   a grammar   might   use   a   rule, which   uses   one   of   its   options, which   uses   one   of   its   symbols          that   is   a   variable, which   would, in   turn, use   another   rule.)
Furthermore, if   we   implement   that   algorithm   using   Python's   generator   functions   — each of   these   methods   yields   a   sequence   of   terminal   symbols, rather   than   returning   them   —               we   can   also   do   this   job   while   using   relatively   little   memory; our   cost   becomes   a   function    of   the   depth   of   the   grammar's   rules   (i.e., how   deeply   we   recurse),   rather   than   the   length       of   the   sentence   we're   generating, which   is   likely   to   be   a   significant   improvement   if   we're    building   long   sentences.
Your   main   module
You   must   have   a   Python   module   named      project4.py, which   provides   a   way   to   execute    your   program   in   whole; executing      project4.py   executes   the   program. Since   you   expect
this   module   to   be   executed   in   this   way, it   would   naturally   need   to   have   an      if            name         ==   '            main            ':   statement at the end of   it, for   reasons   described in your   prior
coursework. Note   that   the   provided   Git   repository   will   already   contain   this   file   (and   the necessary   if   statement).
Modules   other   than   the   main   module
Like   previous   projects, this   is   a   project   that   is   large   enough   that   it   will   benefit   from   being divided   into   separate   modules, each   focusing   on   one   kind   of   functionality,   as   opposed   to    jamming   all   of   it   into   a   single   file   or, worse   yet,   a   single   function. As   before, wFe   aren't               requiring   a   particular   organization, but   we   are   expecting   to   see   that   you   have   "kept
separate   things   separate."
Unlike   in   Project   2   and   Project   3, we   are   not   requiring   the   use   of   Python   packages,   though   you   are   certainly   welcome   to   use   them   if   you'd   like.
Working and testing incrementally
As   you   did   in   previous   projects, you   are   required   to   do   your   work   incrementally, to   test   it incrementally   (i.e., as   you   write   new   functions, you'll   be   implementing   unit   tests   for
them), and   to   commit   your   work   periodically   into   a   Git   repository, which   you   will   be   bundling   and   submitting   to   us.
As   in   those   previous   projects, we   don't   have   a   specific   requirement   about   how   many
commits   you   make, or   how   big   a   "feature" is, but   your   general   goal   is   to   commit   when                you've   reached   stable   ground   — a   new   feature   is   working,   and   you've   tested   it   (including with   unit   test). We'll   expect   to   see   a   history   of   these   kinds   of   incremental   commits.
Testing requirements
Along   with   your   program, you   will   be   required   to   write   unit   tests, implemented   using   the   unittest   module   in   the   Python   standard   library, and   covering   as   much   of   your
program   as   is   practical. As   before, write   your   unit   tests   in   Python   modules   within   a directory named   tests.
As   in   previous   projects, how   you   design   aspects   of   your   program   has   a   positive   impact   on whether   you   can   write   unit   tests   for   it, as   well   as   how   hard   you   might   have   to   work   to   do       it. Your   goal   is   to   cover   as   much   of   your   program   as   is   practical, though,   as   in   recent
projects, there   is   not   a   strict   requirement   around   code   coverage   measurement,   nor   a specific   number   of   tests   that   must   be   written, but   we'll   be   evaluating   whether   your
design   accommodates   your   ability   to   test   it, and   whether   you've   written   unit   tests   that   substantially   cover   the   portions   that   can   be   tested.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
