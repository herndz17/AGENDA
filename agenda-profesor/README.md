# Agenda del profesor de tenis

Página privada (con PIN) donde ves **tus clases del día**, cambias de día, llamas o escribes por WhatsApp al alumno y puedes cancelar una clase.

Es independiente de la web de reservas (`citas-alumnos`), pero **ambas usan la misma base de datos Postgres de Railway** y la misma tabla `reservas`.

## Subirlo a Railway

1. Usa el **mismo proyecto de Railway** donde está tu PostgreSQL y la web de alumnos.
2. Sube esta carpeta a un repositorio de GitHub (distinto al de alumnos).
3. **New → GitHub Repo** y elige este repositorio.
4. En el servicio → **Variables**:
   - `DATABASE_URL` = `${{Postgres.DATABASE_URL}}` (la misma base de datos que usa la web de alumnos)
   - `PROFESOR_PIN` = el PIN que usarás para entrar
   - Opcional: `TZ_NEGOCIO` (America/El_Salvador)
5. **Settings → Networking → Generate Domain**. Ese enlace es solo para ti.

## Probarlo en tu computadora

```bash
npm install
cp .env.example .env     # en Windows: copy .env.example .env
# edita .env: pega la DATABASE_PUBLIC_URL de Railway y elige tu PIN
npm start
```

Abre http://localhost:3000 (usa otro puerto con `PORT=3001 npm start` si también corres la web de alumnos).

## Qué hace

- Muestra las clases activas del día ordenadas por hora, con duración, alumno y notas.
- Navega entre días (‹ › y selector de fecha) y se actualiza solo cada minuto.
- Cancelar una clase la marca como `cancelada` y la hora vuelve a quedar libre para los alumnos.
- Sin PIN correcto no se puede ver ni modificar nada.
