
import telebot
from telebot import types
import logging
from keep_alive import keep_alive  # استيراد دالة keep_alive

# إعداد تسجيل الأخطاء
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

# إعداد التوكن الخاص بالبوت (استبدله بالتوكن الخاص بك)
TOKEN = "7884758906:AAHjXUAkcYWU_TGDowsaRqYsEssJGxdFdh4"

bot = telebot.TeleBot(TOKEN)

# قائمة الأسئلة والإجابات الصحيحة
QUESTIONS = [7
    {
        "question": "متى فرض الصيام على المسلمين؟",
        "options": ["في السنة الأولى للهجرة", "في السنة الثانية للهجرة", "في السنة الثالثة للهجرة", "في السنة الرابعة للهجرة"],
        "answer": "في السنة الثانية للهجرة"
    },
    {
        "question": "ما هو الشهر الذي يأتي بعد رمضان مباشرة؟",
        "options": ["رجب", "ذو القعدة", "شوال", "محرم"],
        "answer": "شوال"
    },
    {
        "question": "أي من الأمور التالية تفطر الصائم؟",
        "options": ["الحجامة", "السواك", "شرب الماء عمدًا", "وضع العطر"],
        "answer": "شرب الماء عمدًا"
    },
    {
        "question": "في أي ليلة يكون تحري ليلة القدر غالبًا؟",
        "options": ["ليلة 25", "ليلة 27", "ليلة 20", "ليلة 15"],
        "answer": "ليلة 27"
    },
    {
        "question": "ما هو أول شيء يفضل أن يفطر عليه الصائم؟",
        "options": ["ماء", "خبز", "تمر", "فواكه"],
        "answer": "تمر"
    },
    {
        "question": "أي من هذه العبادات يكثر المسلمون من أدائها في رمضان؟",
        "options": ["الحج", "الزكاة", "صلاة التراويح", "الأضحية"],
        "answer": "صلاة التراويح"
    },
    {
        "question": "كم عدد الركعات في صلاة التراويح غالبًا؟",
        "options": ["4", "6", "8", "12"],
        "answer": "8"
    },
    {
        "question": "أي من هذه الفئات لا يجب عليها الصيام؟",
        "options": ["الطفل الصغير", "الفقير", "المسافر", "الشاب القادر"],
        "answer": "الطفل الصغير"
    },
    {
        "question": "متى يكون وقت السحور؟",
        "options": ["بعد الفجر", "قبل الفجر", "بعد المغرب", "منتصف الليل"],
        "answer": "قبل الفجر"
    },
    {
        "question": "أي من العبارات التالية صحيحة عن الصيام؟",
        "options": ["يجوز الإفطار لأي شخص دون عذر", "لا يجوز الصيام إلا للمسلمين", "يجوز شرب الماء أثناء الصيام", "يجب الصيام حتى بعد غروب الشمس"],
        "answer": "لا يجوز الصيام إلا للمسلمين"
    },
    {
        "question": "متى يكون موعد الإفطار؟",
        "options": ["عند أذان الفجر", "عند أذان الظهر", "عند أذان المغرب", "عند منتصف الليل"],
        "answer": "عند أذان المغرب"
    },
    {
        "question": "ما هو حكم صيام رمضان؟",
        "options": ["مستحب", "واجب", "مكروه", "مباح"],
        "answer": "واجب"
    },
    {
        "question": "ماذا يحدث إذا أكل الصائم أو شرب ناسيًا؟",
        "options": ["يبطل صيامه", "يجب عليه القضاء", "صيامه صحيح", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو الدعاء الذي يُقال عند الإفطار؟",
        "options": ["اللهم إني أسألك العفو والعافية", "اللهم بارك لنا في هذا الطعام", "اللهم لك صمت وعلى رزقك أفطرت", "لا إله إلا الله وحده لا شريك له"],
        "answer": "اللهم لك صمت وعلى رزقك أفطرت"
    },
    {
        "question": "ما اسم الباب الذي يدخل منه الصائمون إلى الجنة؟",
        "options": ["باب الجنة", "باب الريان", "باب الفردوس", "باب الرحمة"],
        "answer": "باب الريان"
    },
    {
        "question": "كم يوماً يجب أن يصوم المسلم في رمضان؟",
        "options": ["25 يومًا", "30 يومًا", "28 يومًا", "27 يومًا"],
        "answer": "30 يومًا"
    },
    {
        "question": "متى يبدأ شهر رمضان؟",
        "options": ["عند رؤية الهلال", "يوم 1 أبريل", "عند اكتمال القمر", "بعد شهر رجب"],
        "answer": "عند رؤية الهلال"
    },
    {
        "question": "أي من هذه الفئات يجوز لها الإفطار في رمضان؟",
        "options": ["المريض", "الفقير", "الشاب القوي", "الأطفال"],
        "answer": "المريض"
    },
    {
        "question": "متى نزل القرآن على النبي ﷺ لأول مرة؟",
        "options": ["ليلة النصف من شعبان", "ليلة القدر", "أول محرم", "ليلة الإسراء والمعراج"],
        "answer": "ليلة القدر"
    },
    {
        "question": "أي سورة في القرآن تتحدث عن فرضية الصيام؟",
        "options": ["الفاتحة", "البقرة", "المائدة", "النساء"],
        "answer": "البقرة"
    },
    {
        "question": "كم كان عمر النبي ﷺ عندما فرض الصيام؟",
        "options": ["35 سنة", "40 سنة", "45 سنة", "53 سنة"],
        "answer": "53 سنة"
    },
    {
        "question": "ما هو عدد الآيات التي تتحدث عن الصيام في سورة البقرة؟",
        "options": ["3", "5", "7", "9"],
        "answer": "5"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بدون عذر؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "يجب عليه القضاء والكفارة"
    },
    {
        "question": "ما هي الكفارة المترتبة على من أفطر في رمضان بدون عذر؟",
        "options": ["إطعام 10 مساكين", "صيام شهرين متتابعين", "تحرير رقبة", "صيام 60 يومًا"],
        "answer": "صيام شهرين متتابعين"
    },
    {
        "question": "ما هو حكم من نام طوال نهار رمضان؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أكل أو شرب ناسيًا في نهار رمضان؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب المرض؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "يجب عليه القضاء فقط"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب السفر؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "يجب عليه القضاء فقط"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الحمل أو الرضاعة؟",
        "options": ["يجب عليها القضاء فقط", "يجب عليها القضاء والكفارة", "لا شيء عليها", "يجب عليها الكفارة فقط"],
        "answer": "يجب عليها القضاء فقط"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الشيخوخة؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "لا شيء عليه"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الجوع الشديد؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "يجب عليه القضاء فقط"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب العطش الشديد؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "يجب عليه القضاء فقط"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الإكراه؟",
        "options": ["يجب عليه القضاء فقط", "يجب عليه القضاء والكفارة", "لا شيء عليه", "يجب عليه الكفارة فقط"],
        "answer": "لا شيء عليه"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب النسيان؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الخطأ؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الجهل؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الإغماء؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الجنون؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الحيض؟",
        "options": ["صيامها صحيح", "صيامها باطل", "يجب عليها القضاء", "عليها كفارة"],
        "answer": "صيامها باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب النفاس؟",
        "options": ["صيامها صحيح", "صيامها باطل", "يجب عليها القضاء", "عليها كفارة"],
        "answer": "صيامها باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الإغماء الطويل؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الجنون الطويل؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب السكر؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه باطل"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الإغماء الجزئي؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    },
    {
        "question": "ما هو حكم من أفطر في رمضان بسبب الجنون الجزئي؟",
        "options": ["صيامه صحيح", "صيامه باطل", "يجب عليه القضاء", "عليه كفارة"],
        "answer": "صيامه صحيح"
    }, 


]

# حفظ تقدم المستخدمين في الاختبار
user_progress = {}

# دالة لإنشاء قائمة الأزرار الرئيسية
def create_main_menu():
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True, one_time_keyboard=True)
    btn_questions = types.KeyboardButton("الأسئلة 📚")
    btn_other = types.KeyboardButton("ذڪر وزاد ✨")
    markup.add(btn_questions, btn_other)
    return markup

# دالة لإنشاء زر "اضغط هنا للمواصلة"
def create_continue_button():
    markup = types.InlineKeyboardMarkup()
    btn_continue = types.InlineKeyboardButton("➡️ التالي", callback_data="next_question")
    markup.add(btn_continue)
    return markup

# دالة لإنشاء زر "أعد المحاولة"
def create_retry_button():
    markup = types.InlineKeyboardMarkup()
    btn_retry = types.InlineKeyboardButton("🔄 أعد المحاولة", callback_data="retry_question")
    markup.add(btn_retry)
    return markup

# دالة بدء الاختبار عند إرسال /start
@bot.message_handler(commands=['start'])
def start_quiz(message):
    try:
        user_id = message.from_user.id
        user_progress[user_id] = {"score": 0, "current_question": 0, "attempts": 0}

        bot.send_message(message.chat.id, "مرحبًا بك في الاختبار! اختر من القائمة:", reply_markup=create_main_menu())
    except Exception as e:
        logger.error(f"حدث خطأ في start_quiz: {e}")
        bot.send_message(message.chat.id, "حدث خطأ أثناء بدء الاختبار. حاول مرة أخرى لاحقًا.")

# دالة لعرض الأسئلة عند الضغط على "الأسئلة 📚"
@bot.message_handler(func=lambda message: message.text == "الأسئلة 📚")
def show_questions(message):
    try:
        user_id = message.from_user.id
        if user_id not in user_progress:
            bot.send_message(message.chat.id, "يرجى بدء الاختبار بإرسال /start.")
            return

        user_progress[user_id]["current_question"] = 0
        send_question(message.chat.id, user_id)
    except Exception as e:
        logger.error(f"حدث خطأ في show_questions: {e}")
        bot.send_message(message.chat.id, "حدث خطأ أثناء عرض الأسئلة.")

# دالة لإرسال السؤال الحالي
def send_question(chat_id, user_id):
    try:
        user_data = user_progress.get(user_id)
        if not user_data:
            bot.send_message(chat_id, "يرجى بدء الاختبار بإرسال /start.")
            return

        current_question_index = user_data["current_question"]
        if current_question_index < len(QUESTIONS):
            question_data = QUESTIONS[current_question_index]
            markup = types.InlineKeyboardMarkup()

            for option in question_data["options"]:
                button = types.InlineKeyboardButton(option, callback_data=f"answer_{option}")
                markup.add(button)

            bot.send_message(chat_id, f"❓ السؤال {current_question_index + 1}: {question_data['question']}", reply_markup=markup)
        else:
            final_score = user_data["score"]
            total_questions = len(QUESTIONS)
            bot.send_message(chat_id, f"🎉 لقد أكملت الاختبار! نتيجتك: {final_score}/{total_questions}")
    except Exception as e:
        logger.error(f"حدث خطأ في send_question: {e}")
        bot.send_message(chat_id, "حدث خطأ أثناء إرسال السؤال.")

# دالة التحقق من الإجابة عند اختيار خيار
@bot.callback_query_handler(func=lambda call: call.data.startswith("answer_"))
def check_answer(call):
    try:
        user_id = call.from_user.id
        user_data = user_progress.get(user_id)

        if not user_data:
            bot.answer_callback_query(call.id, "يرجى بدء الاختبار بإرسال /start.")
            return

        chosen_answer = call.data.split("_")[1]
        current_question_index = user_data["current_question"]
        correct_answer = QUESTIONS[current_question_index]["answer"]

        bot.delete_message(call.message.chat.id, call.message.message_id)

        if chosen_answer == correct_answer:
            bot.send_message(call.message.chat.id, "✅ إجابة صحيحة! يمكنك المتابعة.", reply_markup=create_continue_button())
            user_data["score"] += 1
            user_data["current_question"] += 1
            user_data["attempts"] = 0
        else:
            user_data["attempts"] += 1
            if user_data["attempts"] >= 3:
                bot.send_message(call.message.chat.id, f"💔 استنفذت جميع محاولاتك.\n✅ الإجابة الصحيحة: {correct_answer}", reply_markup=create_continue_button())
                user_data["current_question"] += 1
                user_data["attempts"] = 0
            else:
                bot.send_message(call.message.chat.id, "❌ إجابة خاطئة! حاول مجددًا.", reply_markup=create_retry_button())
    except Exception as e:
        logger.error(f"حدث خطأ في check_answer: {e}")
        bot.answer_callback_query(call.id, "حدث خطأ أثناء التحقق من الإجابة.")

# دالة الانتقال إلى السؤال التالي
@bot.callback_query_handler(func=lambda call: call.data == "next_question")
def next_question(call):
    try:
        user_id = call.from_user.id
        user_data = user_progress.get(user_id)

        if not user_data:
            bot.send_message(call.message.chat.id, "يرجى بدء الاختبار بإرسال /start.")
            return

        bot.delete_message(call.message.chat.id, call.message.message_id)
        send_question(call.message.chat.id, user_id)
    except Exception as e:
        logger.error(f"حدث خطأ في next_question: {e}")
        bot.send_message(call.message.chat.id, "حدث خطأ أثناء الانتقال للسؤال التالي.")

# دالة إعادة المحاولة
@bot.callback_query_handler(func=lambda call: call.data == "retry_question")
def retry_question(call):
    try:
        user_id = call.from_user.id
        bot.delete_message(call.message.chat.id, call.message.message_id)
        send_question(call.message.chat.id, user_id)
    except Exception as e:
        logger.error(f"حدث خطأ في retry_question: {e}")
        bot.send_message(call.message.chat.id, "حدث خطأ أثناء إعادة المحاولة.")

# تشغيل البوت
if __name__ == "__main__":
    keep_alive()  # تشغيل Flask للحفاظ على التشغيل
    bot.ppolling(none_stop=True) 
