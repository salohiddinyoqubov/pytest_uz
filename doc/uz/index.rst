.. _features:

.. sidebar:: **Keyingi ochiq treninglar va tadbirlar**

    - `Professional Testing with Python <https://python-academy.com/courses/python_course_testing.html>`_, `Python Academy <https://www.python-academy.com/>`_ orqali (3 kunlik chuqurlashtirilgan trening), **2025-yil 4-6-mart**, Leyptsig (DE) / Uzoqdan (online)

    Shuningdek, :doc:`oldingi ma'ruzalar va blogpostlarni <talks>` ham ko'ring.

pytest: yaxshiroq dasturlar yozishga yordam beradi
==================================================

.. toctree::
    :hidden:    

    getting-started
    how-to/index
    reference/index
    explanation/index
    example/index

.. toctree::
    :caption: Loyihaga oid
    :hidden:

    changelog
    contributing
    backwards-compatibility
    sponsor
    tidelift
    license
    contact

.. toctree::
    :caption: Foydali havolalar
    :hidden:

    pytest @ PyPI <https://pypi.org/project/pytest/>
    pytest @ GitHub <https://github.com/pytest-dev/pytest/>
    Issue Tracker <https://github.com/pytest-dev/pytest/issues>
    PDF qo'llanma <https://media.readthedocs.org/pdf/pytest/latest/pytest.pdf>

.. module:: pytest

``pytest`` frameworki kichik, o'qilishi oson testlarni yozishni osonlashtiradi va ilovalar hamda kutubxonalar uchun murakkab funksional testlarni qo'llab-quvvatlashga moslashadi.

``pytest`` uchun Python 3.8+ yoki PyPy3 talab etiladi.

**PyPI paketi nomi**: :pypi:`pytest`

Tezkor misol
------------

.. code-block:: python

    # test_sample.py mazmuni
    def inc(x):
        return x + 1


    def test_answer():
        assert inc(3) == 5

Ishga tushirish:

.. code-block:: pytest

    $ pytest
    =========================== test session starts ============================
    platform linux -- Python 3.x.y, pytest-8.x.y, pluggy-1.x.y
    rootdir: /home/sweet/project
    collected 1 item

    test_sample.py F                                                     [100%]

    ================================= FAILURES =================================
    _______________________________ test_answer ________________________________

        def test_answer():
    >       assert inc(3) == 5
    E       assert 4 == 5
    E        +  where 4 = inc(3)

    test_sample.py:6: AssertionError
    ========================= short test summary info ==========================
    FAILED test_sample.py::test_answer - assert 4 == 5
    ============================ 1 failed in 0.12s =============================

``pytest``'ning batafsil assertion tahlili tufayli faqat oddiy ``assert`` operatorlari ishlatiladi.
:ref:`Boshlash <getstarted>` bo'limida pytest'dan foydalanish asoslari bilan tanishishingiz mumkin.

Xususiyatlar
------------

- Muvaffaqiyatsiz :ref:`assert bayonotlari <assert>` haqida batafsil ma'lumot (``self.assert*`` nomlarini eslab qolish shart emas)
- Test modullari va funksiyalarini :ref:`Avto-topish <test discovery>` imkoniyati
- :ref:`Modulli fixture'lar <fixture>` - kichik yoki parametrli uzoq muddatli test resurslarini boshqarish
- :ref:`unittest <unittest>` (shu jumladan trial) test to'plamlarini darhol ishga tushirish
- Python 3.8+ yoki PyPy 3
- 1300+ dan ortiq :ref:`tashqi plaginlar <plugin-list>` va rivojlanayotgan jamoa bilan kuchli plagin arxitekturasi

Qo'llanma
---------

* :ref:`Boshlash <get-started>` - pytest-ni o'rnating va asoslarini 20 daqiqada o'rganing
* :ref:`Qanday qilib <how-to>` - turli ish holatlari uchun qadam-baqadam qo'llanmalar
* :ref:`Ma'lumotnoma <reference>` - pytest API to'liq ma'lumotnomasi va plaginlar ro'yxati
* :ref:`Tushuntirishlar <explanation>` - asosiy tushunchalar va yuqori darajadagi savollarga javoblar

Xatolar/So'rovlar
-----------------

Xatolarni bildirish yoki yangi xususiyatlarni so'rash uchun `GitHub issue tracker <https://github.com/pytest-dev/pytest/issues>`_ dan foydalaning.

pytest-ni qo'llab-quvvatlash
----------------------------

`Open Collective`_ - ochiq manba loyihalari uchun shaffof moliyalashtirish platformasi. Platforma bir martalik yoki oylik xayr-ehsonlar orqali loyihani qo'llab-quvvatlash imkonini beradi.

Batafsil ma'lumot: `pytest collective`_

.. _Open Collective: https://opencollective.com
.. _pytest collective: https://opencollective.com/pytest

pytest Biznes uchun
--------------------

Tidelift obunasi tarkibida mavjud.

pytest va minglab boshqa paketlarning qo'llab-quvvatlovchilari Tidelift bilan hamkorlikda tijorat dasturlaringiz uchun ochiq manba bog'liqliklarini boshqaradi. Xavfni kamaytiring, kod sifatini oshiring va ishlab chiquvchilarni qo'llab-quvvatlang.

`Batafsil ma'lumot <https://tidelift.com/subscription/pkg/pypi-pytest?utm_source=pypi-pytest&utm_medium=referral&utm_campaign=enterprise&utm_term=repo>`_

Xavfsizlik
~~~~~~~~~~

pytest hech qachon xavfsizlik zaifliklari bilan bog'liq bo'lmagan. Xavfsizlik muammolarini `Tidelift xavfsizlik aloqasi <https://tidelift.com/security>`_ orqali xabar qiling. Tidelift bartaraf etish va oshkor qilishni muvofiqlashtiradi.
