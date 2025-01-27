Tarix
=====

pytest uzun va qiziqarli tarixga ega. Ushbu repozitoriyadagi `birinchi
commit <https://github.com/pytest-dev/pytest/commit/5992a8ef21424d7571305a8d7e2a3431ee7e1e23>`__
2007-yil yanvar oyiga tegishli. Bu commit ham oʻzida koʻp maʼlumotni
saqlaydi: Repozitoriy dastlab :pypi:`py` kutubxonasi (keyinchalik
pytestga ajratilgan) uchun yaratilgan va dastlab SVN, keyin Mercurial,
oxir-oqibat gitga koʻchirilgan.

Commitda “yangi rivojlanish trunkini yaratish” deyilgan va hajmi katta:
*435 ta fayl oʻzgartirilgan, 58640 qator qoʻshilgan*. Buning sababi,
pytest dastlab `PyPy <https://www.pypy.org/>`__ loyihasi tarkibida uning
testlarini yozishni osonlashtirish uchun yaratilgan. Mana uning mustaqil
loyihaga aylanish tarixi:

-  2002-yil oxiri / 2003-yil boshida `PyPy paydo
   boʻldi <https://morepypy.blogspot.com/2018/09/the-first-15-years-of-pypy.html>`__.

-  Blog postda aytilganidek, testlashga dastlab eʼtibor katta edi.
   ``unittest.py`` ustida turli ``testsupport`` fayllari mavjud edi.
   2003-yil iyun oyida Holger Krekel (:user:`hpk42`) `test frameworkini
   qayta
   tuzdi <https://mail.python.org/pipermail/pypy-dev/2003-June/000787.html>`__
   (``pypy.tool.test``, lekin hali ``unittest.py`` asosida).

-  2003-yil dekabrda Stefan Schwarzer tomonidan ``pypy.tool.newtest``
   deb nomlangan `yana bir
   takomillashtirish <https://foss.heptapod.net/pypy/pypy/-/commit/02752373e1b29d89c6bb0a97e5f940caa22bdd63>`__
   amalga oshirildi.

-  Biroq, u uzoq yashamadi. 2004-yil iyun/iyul oylarida ``utest``
   loyihasi boshlandi, oddiy assertlarni taklif qiladi. Bu pytestga
   oʻxshash narsaning boshlanishi boʻlishi mumkin edi, lekin test runner
   kodi aniq emas. Hozirgacha saqlanib qolgan `bu
   fayl <https://foss.heptapod.net/pypy/pypy/-/commit/0735f9ed287ec20950a7dd0a16fc10810d4f6847>`__
   toʻliq test runner emas. Laura Creighton va Samuele Pedroni
   (:user:`pedronis`) mavjud testlarni ``utest`` frameworkiga avtomatik
   oʻtkazishga urinishlari
   `koʻrinadi <https://foss.heptapod.net/pypy/pypy/-/commits/branch/default?utf8=%E2%9C%93&search=utest>`__.

-  Xuddi shu vaqtda, Europython 2004 uchun @hpk42 `“std” deb nomlangan
   loyihani
   boshladi <http://web.archive.org/web/20041020215353/http://codespeak.net/svn/user/hpk/talks/std-talk.txt>`__.
   Bu loyiha keyinchalik pytestga aylangan tamoyillarni belgilab berdi:

      -  Hozirgi “batareyalar bilan birga” foydali, lekin

         -  Ularning baʼzilari, ayniqsa unittest-framework, Java
            uslubida yozilgan
         -  Eng yaxshi API — mavjud boʻlmagan API

      […]

      -  Test paketi minimal shablon kodni talab qilishi va
         moslashuvchan boʻlishi kerak
      -  Yuqori sifatli tracebacklar va debug qoʻllab-quvvatlashni
         taʼminlashi kerak

      […]

      -  Birinchi navbatda… “assertXYZ API” cheklovlarini unutib,
         haqiqiy ``assert``\ dan foydalaning:

         ::

            assert x == y

      -  Bu oddiy Python bilan ishlaydi, lekin maʼlumotsiz “assertion
         failed” xatolari beradi

      -  std.utest (sehrli!) assertion ifodasini qayta talqin qiladi va
         qiymatlar haqida batafsil maʼlumot beradi

-  2004-yil sentyabrda ``py-dev`` mailing listi yaratildi, hozir
   `pytest-dev <https://mail.python.org/pipermail/pytest-dev/>`__ deb
   nomlanadi.

-  2004-yil sentyabr/oktyabr oylarida ``std`` loyihasi `“py” deb
   oʻzgartirildi <https://mail.python.org/pipermail/pypy-dev/2004-September/001565.html>`__,
   ``std.utest`` esa ``py.test``\ ga aylandi. Bu ham `toʻliq manba
   kodi <https://foss.heptapod.net/pypy/pypy/-/commit/42cf50c412026028e20acd23d518bd92e623ac11>`__
   birinchi marta paydo boʻlgan vaqt:

   -  ``py.path.local`` (hozir pytestda pathlibga almashtirilmoqda)
   -  Toʻplam daraxti gʻoyasi: ``Collector``, ``FSCollector``,
      ``Directory``, ``PyCollector``, ``Module``, ``Class``
   -  Argumentlar: ``-x`` / ``--exitfirst``, ``-l`` / ``--showlocals``,
      ``--fulltrace``, ``--pdb``, ``-S`` / ``--nocapture`` (hozir ``-s``
      / ``--capture=off``), ``--collectonly`` (hozir ``--collect-only``)

-  Xuddi shu oyda, ``py`` kutubxonasi `PyPydan
   ajratildi <https://foss.heptapod.net/pypy/pypy/-/commit/6bdafe9203ad92eb259270b267189141c53bce33>`__.

-  2004-yil oktyabrdan (pyni PyPydan olib tashlash) 2007-yil yanvargacha
   (hozirgi pytest repozitoriyasidagi birinchi commit) hech qanday
   faollik koʻrinmadi. Biroq, mailing listda munozaralar boʻlib, `bir
   necha relizlar <py/0.8.0-alpha2/#history>`__ chiqdi:

   -  2006-yil mart: py 0.8.0-alpha2
   -  2007-yil may: py 0.9.0
   -  2008-yil mart: py 0.9.1 (`pytest
      changelogida <https://github.com/pytest-dev/pytest/blob/main/doc/en/changelog.rst#091>`__
      topilgan birinchi reliz)
   -  2008-yil avgust: py 0.9.2

-  2009-yil avgustda py 1.0.0 chiqdi, `asosiy xususiyatlar
   kiritildi <https://holgerkrekel.net/2009/08/04/pylib-1-0-0-released-the-testing-with-python-innovations-continue/>`__:

   -  funcargs/fixtures
   -  `Plugin
      arxitekturasi <http://web.archive.org/web/20090629032718/https://codespeak.net/py/dist/test/extend.html>`__
      (hozirgacha oʻxshash)
   -  `Standart
      pluginlar <http://web.archive.org/web/20091005181132/https://codespeak.net/py/dist/test/plugin/index.html>`__,
      masalan,
      `monkeypatch <http://web.archive.org/web/20091012022829/http://codespeak.net/py/dist/test/plugin/how-to/monkeypatch.html>`__

-  Hatto
   `FAQ <http://web.archive.org/web/20091005222413/http://codespeak.net/py/dist/faq.html>`__\ da
   aytilgan:

      “std” nomi loyihaga zarar yetkazgan boʻlishi mumkin. Loyiha nomi
      oʻzgartirilishi yoki boʻlinishi mumkin.

   Bu 2010-yil noyabrda pytest 2.0.0
   `chiqarilganda <https://mail.python.org/pipermail/pytest-dev/2010-November/001687.html>`__
   amalga oshdi (``py.test`` nomi saqlangan).

-  2016-yil avgustda pytest 3.0.0 chiqdi, unda ``pytest`` (oldingi
   ``py.test`` oʻrniga) asosiy buyruq sifatida tavsiya etildi.

pytestning boshlanish sanasini aniqlash qiyin. Buning uchun Europython
2004 (2004-yil iyun/iyul) boshlangʻich nuqta deb hisoblash mumkin.
