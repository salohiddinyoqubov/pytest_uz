.. _features:

.. yon panel:: **Keyingi ochiq treninglar va tadbirlar**

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

.. modul:: pytest

``pytest`` frameworki kichik, o'qilishi oson testlarni yozishni osonlashtiradi va ilovalar hamda kutubxonalar uchun murakkab funksional testlarni qo'llab-quvvatlashga moslashadi.

``pytest`` uchun Python 3.8+ yoki PyPy3 talab etiladi.

**PyPI paketi nomi**: :pypi:`pytest`

Masalan
------------

.. code-block:: python

    # test_sample.py
    def inc(x):
        return x + 1


    def test_answer():
        assert inc(3) == 5


Buni bajarish uchun:


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

``pytest``'ning batafsil assertion tahlil qilish imkoniyati tufayli faqat oddiy ``assert`` operatorlari ishlatiladi.
:ref:`Boshlash <getstarted>` bo'limida pytest'dan foydalanishni asosiy ko'rsatmalar bilan tanishing.

Xususiyatlar
------------

- Muvaffaqiyatsiz :ref:`assert operatorlari <assert>` haqida batafsil ma'lumot (``self.assert*`` nomlarini eslab qolish shart emas)

- Test modullari va funksiyalarini :ref:`Avto-aniqlash <test discovery>` imkoniyati

- Kichik yoki parametrli uzoq muddatli test resurslarini boshqarish uchun :ref:`Modulli fixture'lar <fixture>`

- Parallel ravishda testlarni bajarish imkoniyati

- Kuchli plagin arxitekturasi orqali yangi imkoniyatlarni qo'shish qulayligi

- Yaxshi dokumentatsiya va keng jamoat tomonidan qo'llab-quvvatlanish imkoniyati

Qo'shimcha ma'lumotlar uchun pytestning :ref:`Rasmiy qo'llanma <reference/index>` bo'limini o'rganing.

Qo'llanma
---------

* :ref:`Boshlash <get-started>` - pytest-ni o'rnatish va uning asoslarini bor-yo'g'i yigirma daqiqada o'rganing
* :ref:`Qanday qilib <how-to>` - qadam-baqadam qo'llanmalar, ko'plab ish holatlari va ehtiyojlarni qamrab oladi
* :ref:`Ma'lumotlar <reference>` - pytest API to'liq ma'lumotnomasini, plaginlar ro'yxatini va boshqalarni o'z ichiga oladi
* :ref:`Tushuntirish <explanation>` - asosiy mavzular muhokamasi, yuqori darajadagi savollarga javoblar va boshqa tushuntirishlar

Xatolar/Yozuvlar
----------------

Iltimos, xatolarni yoki yangi imkoniyatlar takliflarini yuborish uchun `GitHub issues'ga o'ting <https://github.com/pytest-dev/pytest/issues>`_ dan foydalaning.

pytest-ni qo‘llab-quvvatlash
-----------------------------

`Open Collective`_ — ochiq va shaffof jamiyatlar uchun onlayn moliyalashtirish platformasi.
Bu platforma mablag' to'plash va moliyaviy ko'rsatkichlarni to'liq shaffof tarzda bo'lishish vositalarini taqdim etadi.

Bu platforma bir martalik yoki oylik xayr-ehsonlarni to'g'ridan-to'g'ri loyihaga yubormoqchi bo'lgan shaxslar va kompaniyalar uchun qulay.

Batafsil ma'lumotni `pytest collective`_ sahifasida topishingiz mumkin.

.. _Open Collective: https://opencollective.com
.. _pytest collective: https://opencollective.com/pytest

pytest uchun muvaffaqiyatsiz test_sample.py::test_answer - assert 4 == 5
------------------------------------------------------------------------

Tidelift Subscription orqali mavjud.

pytest va boshqa minglab paketlarning texnik xizmat ko'rsatuvchilari Tidelift bilan hamkorlik qilib,
tijorat qo‘llab-quvvatlashi va ochiq manba ilovalariga bog‘liq paketlarga xizmat ko‘rsatishni ta’minlashmoqda.
Bu yordam sizning vaqtingizni tejaydi, xavfni kamaytiradi va kod sifatini yaxshilaydi,
shu bilan birga aynan o'zingiz ishlatayotgan bog'liqliklarni ishlab chiqayotgan texnik xizmat ko'rsatuvchilarni qo'llab-quvvatlaysiz.

`Batafsil bilib oling. <https://tidelift.com/subscription/pkg/pypi-pytest?utm_source=pypi-pytest&utm_medium=referral&utm_campaign=enterprise&utm_term=repo>`_

Xavfsizlik
~~~~~~~~~~

pytest xavfsizlikka oid muammolar bilan hech qachon bog‘liq bo‘lmagan, ammo har qanday holatda
xavfsizlik kamchiligini xabar qilish uchun `Tidelift xavfsizlik kontaktlari <https://tidelift.com/security>`_ dan foydalaning.
Tidelift kamchilikni tuzatish va uni oshkor qilish jarayonini muvofiqlashtiradi.
