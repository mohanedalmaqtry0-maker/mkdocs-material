from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle, PageBreak
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib import colors

# إعداد ملف PDF
file_path = "/mnt/data/منهج_تحليل_الأفلام.pdf"
doc = SimpleDocTemplate(file_path, pagesize=A4)

styles = getSampleStyleSheet()
styles.add(ParagraphStyle(name='TitleStyle', fontName='Helvetica-Bold', fontSize=18, spaceAfter=12, alignment=1))
styles.add(ParagraphStyle(name='HeadingStyle', fontName='Helvetica-Bold', fontSize=14, spaceAfter=8, spaceBefore=12))
styles.add(ParagraphStyle(name='BodyStyle', fontName='Helvetica', fontSize=11, leading=16, spaceAfter=6))

content = []

# العنوان الرئيسي
content.append(Paragraph("منهج تدريبي موسع لتحليل الأفلام", styles['TitleStyle']))
content.append(Spacer(1, 12))

# المقدمة
content.append(Paragraph("المقدمة", styles['HeadingStyle']))
content.append(Paragraph("""
هذا الدليل يهدف إلى تحويلك من مشاهد عادي إلى محلل سينمائي محترف. 
سيساعدك على النظر إلى الفيلم كعملية متكاملة تشمل الإخراج، التمثيل، التصوير، الأزياء، الموسيقى، المونتاج، 
وحتى الرسائل الرمزية والثقافية. صُمم هذا المنهج كأداة عملية تشبه منهج أكاديمية سينما عالمية.
""", styles['BodyStyle']))

# خلف الكواليس
content.append(Paragraph("القسم الأول: خلف الكواليس", styles['HeadingStyle']))
backstage_points = [
    ("المخرج", "بصمته الخاصة، تكرار الأسلوب، رؤية إخراجية متسقة."),
    ("السيناريو", "بنية القصة، بناء الشخصيات، الحوار."),
    ("الإنتاج والتمويل", "تأثير الميزانية على نوعية الفيلم."),
    ("أماكن التصوير", "رمزية المكان، هل المكان واقعي أم استوديو."),
    ("الأزياء والماكياج", "انعكاس الشخصية والزمن التاريخي."),
    ("التصوير السينمائي", "العدسات، حركة الكاميرا، الألوان."),
    ("الإضاءة", "الظلال، توزيع الضوء، الإحساس النفسي."),
    ("الموسيقى التصويرية", "تأثيرها على الحالة الشعورية."),
    ("المؤثرات البصرية", "هل تخدم القصة أم مجرد بهرجة."),
    ("اختيار الممثلين", "مناسبتهم للأدوار، ممثلون جدد أو مخضرمون."),
    ("المونتاج", "الإيقاع، السرد البصري، التوازي بين المشاهد."),
]
for title, desc in backstage_points:
    content.append(Paragraph(f"<b>{title}</b>: {desc}", styles['BodyStyle']))

content.append(PageBreak())

# داخل الفيلم
content.append(Paragraph("القسم الثاني: داخل الفيلم", styles['HeadingStyle']))
inside_points = [
    ("المغزى والموضوع", "القضية الكبرى التي يناقشها الفيلم."),
    ("الرمزية", "الألوان، الأشياء الصغيرة، الرموز المتكررة."),
    ("الحوار", "الجمل المفتاحية، الصمت كأداة درامية."),
    ("اللغة السينمائية", "الصورة بدلاً من الكلام، حركة الكاميرا."),
    ("الأخطاء", "مقصودة لكسر القاعدة أو غير مقصودة."),
    ("الثقافة والمعرفة", "المدن، اللهجات، العادات الاجتماعية."),
    ("بناء الشخصيات", "القوس الدرامي وتطور الشخصية."),
    ("التوقيت والإيقاع", "طول اللقطات، توقيت القطع."),
    ("التفاصيل الصغيرة", "الأشياء في الخلفية والرموز المخفية."),
    ("التأثير الشخصي", "ما الذي ألهمك أو غير نظرتك."),
]
for title, desc in inside_points:
    content.append(Paragraph(f"<b>{title}</b>: {desc}", styles['BodyStyle']))

content.append(PageBreak())

# أوراق العمل (جداول)
content.append(Paragraph("القسم الثالث: أوراق عمل عملية", styles['HeadingStyle']))
data = [
    ["المحور", "ماذا تلاحظ", "أسئلة موجهة", "ملاحظاتي"],
    ["التمثيل", "لغة الجسد، التعابير", "هل الأداء طبيعي أم مبالغ فيه؟", ""],
    ["الإخراج", "طريقة السرد، ترتيب المشاهد", "هل المخرج يكرر أسلوبه؟", ""],
    ["التصوير", "نوع اللقطة، الحركة", "هل الزاوية تعكس معنى معين؟", ""],
    ["الإضاءة", "الظلال، التباين", "هل النور والظلام يعكسان صراعًا داخليًا؟", ""],
    ["الموسيقى", "موسيقى، أصوات، صمت", "ماذا يحدث لو أزلنا الموسيقى؟", ""],
]
table = Table(data, repeatRows=1, colWidths=[80, 130, 130, 100])
table.setStyle(TableStyle([
    ("BACKGROUND", (0, 0), (-1, 0), colors.grey),
    ("TEXTCOLOR", (0, 0), (-1, 0), colors.whitesmoke),
    ("ALIGN", (0, 0), (-1, -1), "CENTER"),
    ("FONTNAME", (0, 0), (-1, 0), "Helvetica-Bold"),
    ("BOTTOMPADDING", (0, 0), (-1, 0), 10),
    ("GRID", (0, 0), (-1, -1), 0.5, colors.black),
]))
content.append(table)

content.append(PageBreak())

# نصائح الخبراء
content.append(Paragraph("القسم الرابع: نصائح الخبراء", styles['HeadingStyle']))
expert_tips = [
    "شاهد الفيلم ثلاث مرات: مرة كمشاهد عادي، مرة كفني، مرة كناقد.",
    "اربط العناصر: (الإضاءة + الموسيقى + الأزياء) = معنى مركب.",
    "حلل دقيقة واحدة من فيلم: استخرج 5 عناصر مخفية.",
    "قارن بين أفلام المخرج نفسه لاكتشاف بصمته الإبداعية.",
]
for tip in expert_tips:
    content.append(Paragraph(f"- {tip}", styles['BodyStyle']))

content.append(PageBreak())

# الخاتمة
content.append(Paragraph("الخاتمة", styles['HeadingStyle']))
content.append(Paragraph("""
التحليل السينمائي ليس مجرد ملاحظة سطحية، بل هو تدريب ذهني يفتح لك فهمًا أعمق للفن والثقافة 
ويجعلك تفكر كالمخرج والممثل والناقد في الوقت ذاته. 
استخدم هذا الدليل كأداة مستمرة لتطوير أسلوبك النقدي الخاص وصقل رؤيتك السينمائية.
""", styles['BodyStyle']))

# بناء الملف
doc.build(content)
file_path
