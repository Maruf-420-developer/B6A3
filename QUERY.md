SELECT
    b.id AS booking_id,
    u.name AS customer_name,
    v.vehicle_name,
    b.start_date,
    b.end_date,
    b.status
FROM bookings b
INNER JOIN "user" u ON b.user_id = u.id
INNER JOIN vehicle v ON b.vehicle_id = v.id
ORDER BY b.id;

SELECT
    v.id AS vehicle_id,
    v.vehicle_name,
    v.type,
    v.model,
    v.reg_number,
    v.rental_price,
    v.availability_status
FROM vehicle v
WHERE NOT EXISTS (
    SELECT 1
    FROM bookings b
    WHERE b.vehicle_id = v.id
);

SELECT
    v.id AS vehicle_id,
    v.vehicle_name,
    v.type,
    v.model,
    v.reg_number,
    v.rental_price,
    v.availability_status
FROM vehicle v
WHERE v.availability_status = 'available'
  AND v.type = 'car';

SELECT
    v.vehicle_name,
    COUNT(b.id) AS total_bookings
FROM bookings b
INNER JOIN vehicle v ON b.vehicle_id = v.id
GROUP BY v.vehicle_name
HAVING COUNT(b.id) > 2;
