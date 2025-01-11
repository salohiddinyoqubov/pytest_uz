.. _get-started:

Boshlash
===================================

.. _`getstarted`:
.. _`installation`:

``pytest`` ni o‘rnatish
----------------------------------------

``pytest`` quyidagilarni talab qiladi: Python 3.8+ yoki PyPy3.

1. Buyruqlar qatorida quyidagi buyruqni ishga tushiring:

.. code-block:: bash

    pip install -U pytest

2. To‘g‘ri versiyani o‘rnatganingizni tekshiring:

.. code-block:: bash

    $ pytest --version
    pytest 8.3.3

.. _`simpletest`:

Birinchi testni yarating
----------------------------------------------------------

``test_sample.py`` nomli yangi fayl yarating, u funksiya va testni o‘z ichiga oladi:

.. code-block:: python

    # test_sample.py mazmuni
    def func(x):
        return x + 1


    def test_answer():
        assert func(3) == 5

Testni ishga tushiring:

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
    >       assert func(3) == 5
    E       assert 4 == 5
    E        +  where 4 = func(3)

    test_sample.py:6: AssertionError
    ========================= short test summary info ==========================
    FAILED test_sample.py::test_answer - assert 4 == 5
    ============================ 1 failed in 0.12s =============================

``[100%]`` barcha test holatlarini ishga tushirish jarayonidagi umumiy progressni bildiradi. Test yakunlangandan so‘ng, pytest ``func(3)`` ``5`` qiymatini qaytarmagani uchun muvaffaqiyatsizlik hisoboti ko‘rsatadi.

.. note::

    Test natijalarini tasdiqlash uchun ``assert`` bayonotidan foydalanishingiz mumkin. pytest’ning :ref:`Ilg‘or tasdiq introspektsiyasi <python:assert>` ifoda orasidagi qiymatlarni aqlli tarzda hisobot qiladi va bu orqali :ref:`JUnit usullarining ko‘plab nomlaridan <testcase-objects>` foydalanishdan qochishingiz mumkin.

Bir nechta testlarni ishga tushirish
----------------------------------------------------------

``pytest`` joriy katalogdagi va uning ostidagi kataloglardagi ``test_*.py`` yoki ``*_test.py`` shaklidagi barcha fayllarni ishga tushiradi. Umuman olganda, u :ref:`standart testlarni aniqlash qoidalariga <test discovery>` amal qiladi.

Ma’lum bir xatolik qayd etilganini tasdiqlash
--------------------------------------------------------------

Xatolik qayd etilishini tasdiqlash uchun :ref:`raises <assertraises>` yordamchisidan foydalaning:

.. code-block:: python

    # test_sysexit.py mazmuni
    import pytest


    def f():
        raise SystemExit(1)


    def test_mytest():
        with pytest.raises(SystemExit):
            f()

:ref:`raises <assertraises>` tomonidan taqdim etilgan kontekstdan foydalanib, :class:`ExceptionGroup` tarkibida kutgan xatolik borligini tasdiqlash mumkin:

.. code-block:: python

    # test_exceptiongroup.py mazmuni
    import pytest


    def f():
        raise ExceptionGroup(
            "Guruh xabari",
            [
                RuntimeError(),
            ],
        )


    def test_exception_in_group():
        with pytest.raises(ExceptionGroup) as excinfo:
            f()
        assert excinfo.group_contains(RuntimeError)
        assert not excinfo.group_contains(TypeError)

Test funksiyasini “quiet” rejimida ishga tushiring:

.. code-block:: pytest

    $ pytest -q test_sysexit.py
    .                                                                    [100%]
    1 passed in 0.12s

.. note::

    ``-q/--quiet`` flagidan foydalanish natijasida qisqa chiqish olinadi.

Bir nechta testlarni class'da guruhlash
--------------------------------------------------------------

Bir nechta testlarni ishlab chiqqaningizdan so‘ng, ularni class'da guruhlashni xohlashingiz mumkin. pytest buni oson qiladi:

.. code-block:: python

    # test_class.py mazmuni
    class TestClass:
        def test_one(self):
            x = "bu"
            assert "b" in x

        def test_two(self):
            x = "salom"
            assert hasattr(x, "check")

``pytest`` barcha ``test_`` bilan boshlanuvchi funksiyalarni aniqlaydi. Class'ni ``Test`` bilan nomlashni unutmang, aks holda class o‘tkazib yuboriladi. Modulni quyidagi buyruq orqali ishga tushiring:

.. code-block:: pytest

    $ pytest -q test_class.py
    .F                                                                   [100%]
    ================================= FAILURES =================================
    ____________________________ TestClass.test_two ____________________________

    self = <test_class.TestClass object at 0xdeadbeef0001>

        def test_two(self):
            x = "salom"
    >       assert hasattr(x, "check")
    E       AssertionError: assert False
    E        +  where False = hasattr('salom', 'check')

    test_class.py:8: AssertionError
    ========================= short test summary info ==========================
    FAILED test_class.py::TestClass::test_two - AssertionError: assert False
    1 failed, 1 passed in 0.12s

Testlarni class'larda guruhlash quyidagi sabablar uchun foydali bo‘lishi mumkin:

 * Testlarni tashkil qilish
 * Faqat ushbu class'dagi testlar uchun fixture’lardan foydalanish
 * Belgilarni class darajasida qo‘llash va ularning barcha testlarga tatbiq qilinishi

Class'larda testlarni guruhlaganingizda, har bir test class'ning o‘ziga xos namunasi bilan ishlashini unutmang. Bu testlarni izolyatsiya qilishni ta’minlaydi va yomon amaliyotlarning oldini oladi.

Yana davom ettirish
-------------------------------------

Qo‘shimcha pytest manbalarini ko‘rib chiqing:

* ":ref:`usage`" - buyruqlar misollari uchun
* ":ref:`existingtestsuite`" - mavjud testlar bilan ishlash uchun
* ":ref:`mark`" - ``pytest.mark`` mexanizmi haqida
* ":ref:`fixtures`" - testlaringiz uchun funktsional asosni ta’minlash
* ":ref:`plugins`" - plaginlarni boshqarish va yozish uchun
* ":ref:`goodpractices`" - virtualenv va testlarni tashkil qilish
