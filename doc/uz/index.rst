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

.. module:: pytest

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

- Muvaffaqiyatsiz :ref:`assert bayonotlari <assert>` haqida batafsil ma'lumot (``self.assert*`` nomlarini eslab qolish shart emas)

- Test modullari va funksiyalarini :ref:`Avto-aniqlash <test discovery>` imkoniyati

- Kichik yoki parametrli uzoq muddatli test resurslarini boshqarish uchun :ref:`Modulli fixture'lar <fixture>`

- :ref:`unittest <unittest>` (shu jumladan trial) test to'plamlarini bir zumda bajarish imkoniyati

- Python 3.8+ yoki PyPy 3

- 1300+ dan ortiq :ref:`tashqi plaginlar <plugin-list>` va rivojlanayotgan jamoa orqali kuchli plagin arxitekturasi


Qo'llanma
----------

* :ref:`Boshlash <get-started>` - pytest-ni o'rnating va uning asoslarini atigi yigirma daqiqada o'rganing
* :ref:`Qanday qilib <how-to>` - qadam-baqadam qo'llanmalar, turli ish holatlari va ehtiyojlarni qamrab oladi
* :ref:`Ma'lumotlar <reference>` - pytest API to'liq ma'lumotnomasini, plaginlar ro'yxatini va boshqalarni o'z ichiga oladi
* :ref:`Tushuntirish <explanation>` - asosiy mavzularni tushuntirish, yuqori darajadagi savollarga javoblar


Xatolar/Talablar
----------------

Iltimos, xatolarni yuborish yoki xususiyatlar so'rash uchun `GitHub issue tracker <https://github.com/pytest-dev/pytest/issues>`_ dan foydalaning.

pytest-ni qo'llab-quvvatlash
----------------------------

`Open Collective`_ — ochiq va shaffof jamiyatlar uchun onlayn moliyalashtirish platformasi.
Bu platforma mablag' to'plash va moliyaviy ko'rsatkichlarni to'liq shaffof tarzda bo'lishish vositalarini taqdim etadi.

Bu platforma bir martalik yoki oylik xayr-ehsonlarni to'g'ridan-to'g'ri loyihaga yubormoqchi bo'lgan shaxslar va kompaniyalar uchun qulay.

Batafsil ma'lumotni `pytest collective`_ sahifasida topishingiz mumkin.

.. _Open Collective: https://opencollective.com
.. _pytest collective: https://opencollective.com/pytest

pytest Biznes uchun
--------------------

Tidelift obunasining bir qismi sifatida mavjud.

pytest va boshqa minglab paketlarni boshqaruvchi mutaxassislar Tidelift bilan hamkorlik qilib,
ochiq manba bog'liqliklarining tijorat qo'llab-quvvatlashi va texnik xizmat ko'rsatishni ta'minlashmoqda.
Bu biznesingiz uchun vaqtni tejash, xavfni kamaytirish va kod sifatini yaxshilash imkonini beradi,
shu bilan birga aynan biznesingizda foydalanayotgan bog'liqliklaringizni ishlab chiqayotgan texnik xizmat ko'rsatuvchilarga moliyaviy qo'llab-quvvatlashni ta'minlaydi.


`Batafsil bilib oling. <https://tidelift.com/subscription/pkg/pypi-pytest?utm_source=pypi-pytest&utm_medium=referral&utm_campaign=enterprise&utm_term=repo>`_

Xavfsizlik
~~~~~~~~~~

pytest hech qachon xavfsizlik zaifliklari bilan bog'liq bo'lmagan, ammo har qanday xavfsizlik muammosi yuzaga kelsa,
iltimos, xavfsizlik zaifliklarini xabar qilish uchun `Tidelift xavfsizlik aloqasi <https://tidelift.com/security>`_ dan foydalaning.
Tidelift ushbu muammoni bartaraf etish va uning oshkor qilinishini samarali tarzda muvofiqlashtiradi.

