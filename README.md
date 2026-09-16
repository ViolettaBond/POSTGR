# POSTGR

CREATE TABLE blog_posts (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    category VARCHAR(100) NOT NULL,
    author_name VARCHAR(150) NOT NULL,
    publication_date DATE NOT NULL,
    reading_time INTEGER NOT NULL,
    introduction TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE blog_sections (
    id SERIAL PRIMARY KEY,
    post_id INTEGER NOT NULL REFERENCES blog_posts(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    sort_order INTEGER NOT NULL
);

CREATE INDEX idx_blog_posts_slug ON blog_posts(slug);
CREATE INDEX idx_blog_sections_post_id ON blog_sections(post_id);

INSERT INTO blog_posts
    (title, slug, category, author_name, publication_date, reading_time, introduction)
VALUES
    (
        'Artificial Intelligence in Healthcare: Transforming Patient Care',
        'artificial-intelligence-in-healthcare',
        'Healthcare',
        'Dr. Emily Walker',
        '2023-10-15',
        10,
        'Artificial Intelligence (AI) has emerged as a transformative force in the healthcare industry, reshaping patient care, diagnostics, and research. In this post, we explore the profound impact of AI in healthcare, from revolutionizing diagnostic accuracy to enhancing patient outcomes.'
    );

INSERT INTO blog_sections (post_id, title, content, sort_order)
VALUES
    (
        1,
        'Artificial Intelligence (AI)',
        'Artificial Intelligence (AI) has permeated virtually every aspect of our lives, and healthcare is no exception. The integration of AI in healthcare is ushering in a new era of medical practice, where machines complement the capabilities of healthcare professionals, ultimately improving patient outcomes and the efficiency of the healthcare system. In this blog post, we will delve into the diverse applications of AI in healthcare, from diagnostic imaging to personalized treatment plans, and address the ethical considerations surrounding this revolutionary technology.',
        1
    ),
    (
        1,
        'AI in Diagnostic Imaging',
        'One of the most prominent applications of AI in healthcare is in diagnostic imaging. AI algorithms have demonstrated remarkable proficiency in interpreting medical images such as X-rays, MRIs, and CT scans. They can identify anomalies and deviations that might be overlooked by the human eye. This is particularly valuable in early disease detection. For instance, AI can aid radiologists in detecting minute irregularities in mammograms or identifying critical findings in chest X-rays, potentially indicative of life-threatening conditions.',
        2
    ),
    (
        1,
        'Predictive Analytics and Disease Prevention',
        'Predictive analytics uses patient data and machine learning models to identify patterns associated with disease risk. This can help healthcare teams recognize potential problems earlier and choose appropriate preventive measures.',
        3
    ),
    (
        1,
        'Personalized Treatment Plans',
        'AI can combine clinical history, laboratory results, imaging data, and other information to help physicians create treatment plans that are better adapted to an individual patient.',
        4
    ),
    (
        1,
        'Drug Discovery and Research',
        'Machine learning can analyze large biological and chemical datasets, helping researchers identify promising compounds and potential drug candidates faster than traditional approaches alone.',
        5
    ),
    (
        1,
        'AI in Telemedicine',
        'AI-powered tools can support remote healthcare by assisting with symptom assessment, patient monitoring, documentation, and prioritization of cases that may require professional attention.',
        6
    ),
    (
        1,
        'Ethical Considerations',
        'The use of AI in healthcare raises important questions about privacy, security, transparency, bias, accountability, and the role of human professionals in clinical decision-making.',
        7
    ),
    (
        1,
        'The Future of AI in Healthcare',
        'As AI technology continues to develop, its role in healthcare is likely to expand. The most useful systems will work alongside medical professionals and remain focused on safety, evidence, and better patient outcomes.',
        8
    ),
    (
        1,
        'Conclusion',
        'Artificial Intelligence is changing healthcare by providing new tools for diagnosis, prediction, personalization, research, and remote care. Its successful adoption depends on combining technological progress with responsible clinical practice.',
        9
    );


CREATE TABLE articles (
    id SERIAL PRIMARY KEY,
    author_key VARCHAR(50) NOT NULL,
    author_name VARCHAR(100) NOT NULL,
    category VARCHAR(50) NOT NULL,
    publish_date DATE NOT NULL,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    image_key VARCHAR(50),
    is_featured BOOLEAN DEFAULT FALSE,
    post_id INT REFERENCES posts(id)
);

INSERT INTO articles (author_key, author_name, category, publish_date, title, description, image_key, is_featured, post_id)
VALUES
('john', 'Jane Smith', 'Environment', '2023-10-15',
 'Global Climate Summit Addresses Urgent Climate Action',
 'World leaders gathered at the Global Climate Summit to discuss urgent climate action, emissions reductions, and renewable energy targets.',
 'global', TRUE, 1),

('sarah', 'Sarah Ethicist', 'Politics', '2023-10-14',
 'A Decisive Victory for Progressive Policies',
 'A deep dive into the recent political shifts.',
 'politics', FALSE, 1),

('john', 'John Techson', 'Technology', '2023-10-13',
 'Tech Giants Unveil Cutting-Edge AI Innovations',
 'Exploring the newest AI breakthroughs from leading tech companies.',
 'technology', FALSE, 1),

('astronomer', 'Dr. Emily', 'Health', '2023-10-12',
 'COVID-19 Variants',
 'The latest research on COVID-19 variants and vaccine effectiveness.',
 'health', FALSE, 1),

('john', 'John Techson', 'Technology', '2023-10-15',
 'Tech Giants Announce New Product Line',
 'Explore the latest innovations from tech industry leaders, unveiling new products that promise to transform the digital landscape',
 NULL, FALSE, 1),

('sarah', 'Sarah Ethicist', 'Technology', '2023-10-11',
 'The Future of Autonomous Vehicles',
 'An in-depth analysis of the rapid advancements in autonomous vehicle technology and their impact on transportation.',
 NULL, FALSE, 1),

('astronomer', 'Astronomer X', 'Technology', '2023-12-10',
 'Tech Startups Secure Record Funding',
 'An overview of the recent surge in funding for tech startups, shaping the entrepreneurial landscape.',
 NULL, FALSE, 1);


CREATE TABLE video (
    id SERIAL PRIMARY KEY,
    cover_key VARCHAR(50) NOT NULL,
    title VARCHAR(255) NOT NULL,
    description TEXT
);

INSERT INTO video (cover_key, title, description)
VALUES
('mars', 'Mars Exploration: Unveiling Alien Landscapes',
 'Embark on a journey through the Red Planet''s breathtaking landscapes and uncover the mysteries of Mars.'),

('blockchain', 'Blockchain Explained: A Revolution in Finance',
 'Delve into the world of blockchain technology and its transformative impact on the financial industry.'),

('mental', 'Breaking the Silence: Mental Health Awareness in the Workplace',
 'An exploration of the importance of mental health awareness and the initiatives reshaping workplaces for employee well-being.'),

('invest', 'Revolutionizing Investment Strategies',
 'An in-depth look at global efforts to conserve biodiversity and safeguard endangered species from extinction.');



CREATE TABLE contact_requests (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(50),
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE faq (
    id SERIAL PRIMARY KEY,
    question TEXT NOT NULL,
    answer TEXT NOT NULL,
    sort_order INT DEFAULT 0
);

INSERT INTO faq (question, answer, sort_order) VALUES
('What is AI?', 'AI stands for Artificial Intelligence, which refers to the simulation of human intelligence in machines. It enables them to perform tasks like problem-solving, learning, and decision-making.', 1),
('How can I listen to your podcasts?', 'You can listen on our website, Spotify, Apple Podcasts, Google Podcasts, and YouTube.', 2),
('Are your podcasts free to listen to?', 'Yes, all our podcasts are completely free.', 3),
('Can I download episodes to listen offline?', 'Yes, you can download episodes directly from the episode page.', 4),
('How often do you release new episodes?', 'We release a new episode every week on Wednesday.', 5);
