# ATS
It is an ATS score checker application.

code:
import PyPDF2
def extract_pages(pdf_path):
  extracted_text=""
  with open(pdf_path,'rb') as file:
    reader=PyPDF2.PdfReader(pdf_path)
  for page in reader.pages:
    page_text=page.extract_text()
    if page_text:
      extracted_text+=page_text
  return extracted_text
def parse_resume(extracted_text):
    prompt = f"""
You are a resume parser.

Extract:
- Skills
- Experience summary
- Education
- Tools & technologies

Resume:
{extracted_text}

Return in bullet points.
"""
    response = Client.models.generate_content(
        model="gemini-2.5-flash",
        contents=prompt
    )
    return response.text
pdf_path='Resume.pdf'
extracted_text=extract_pages(pdf_path)
print(parse_resume(extracted_text))
