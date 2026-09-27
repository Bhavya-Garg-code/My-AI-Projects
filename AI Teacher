from openai import OpenAI
import time
import streamlit as  st
api = st.secrets["API_KEY"]
client = OpenAI(api_key = api,base_url = 
"https://api.groq.com/openai/v1")
model = 'openai/gpt-oss-20b'

def generate(prompt, tokens = 1024):
 try:
    response = client.chat.completions.create(
        model = model,
        messages = [{'role':'user','content':prompt}],
        temperature=0.3,
        max_tokens = tokens
    )
    return response.choices[0].message.content
 except Exception as e:
   return f'Error Occured : {e}'

st.set_page_config(page_title = 'AI Teaching assitant' , layout = 'centered')
st.title("AI Teacher")
st.write("Ask me any question..")
if 'history' not in st.session_state:
  st.session_state.history = []

ques = st.text_input("Enter your question: ")
if st.button('Generate'):
  if(ques.strip()):
    with st.spinner('Generating....'):
         answer = generate(ques)
    st.session_state.history.insert(0,{'question':ques, 'answer':answer})

  else:
     st.warning("No question found!!")

if(st.session_state.history):
   st.markdown(" Conversation history.")
   for i,chat in enumerate(st.session_state.history,1):
      st.markdown(f'Q{i}: {chat["question"]}') 
      st.write(chat['answer'])
      st.divider()
if(st.button("Clear conversation")):
   st.session_state.history = []
   st.rerun()

