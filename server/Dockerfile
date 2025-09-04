FROM python:3.12.0-slim-bookworm

# Supaya Python tidak buffer & selalu write bytecode
ENV PYTHONBUFFERED=1
ENV PYTHONWRITEBYTECODE=1

# Set lokasi aplikasi
ENV APP=/app

# Ubah working directory
WORKDIR $APP

# Tambahkan requirements.txt
COPY requirements.txt $APP

# Install dependency
RUN pip3 install --upgrade pip && pip3 install -r requirements.txt

# Copy semua file project ke container
COPY . $APP

# Expose port untuk Django/Gunicorn
EXPOSE 8000

# Biar entrypoint.sh bisa dijalankan
RUN chmod +x /app/entrypoint.sh

# Jalankan entrypoint
ENTRYPOINT ["/bin/bash","/app/entrypoint.sh"]

# Command default (jalankan Gunicorn)
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]
